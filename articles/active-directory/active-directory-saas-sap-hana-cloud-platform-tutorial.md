---
title: 'Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform | Microsoft Docs'
description: Learn how to use SAP HANA Cloud Platform with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: ffcad259c2cd49ba0f59e15e7f499cba0277f14d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662663"
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a><span data-ttu-id="d41f4-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="d41f4-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform</span></span>
<span data-ttu-id="d41f4-104">The objective of this tutorial is to show the integration of Azure and SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="d41f4-104">The objective of this tutorial is to show the integration of Azure and SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="d41f4-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="d41f4-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="d41f4-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="d41f4-106">A valid Azure subscription</span></span>
* <span data-ttu-id="d41f4-107">A SAP HANA Cloud Platform account</span><span class="sxs-lookup"><span data-stu-id="d41f4-107">A SAP HANA Cloud Platform account</span></span>

<span data-ttu-id="d41f4-108">After completing this tutorial, the Azure AD users you have assigned to SAP HANA Cloud Platform will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d41f4-108">After completing this tutorial, the Azure AD users you have assigned to SAP HANA Cloud Platform will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="d41f4-109">You need to deploy your own application or subscribe to an application on your SAP HANA Cloud Platform account to test single sign on.</span><span class="sxs-lookup"><span data-stu-id="d41f4-109">You need to deploy your own application or subscribe to an application on your SAP HANA Cloud Platform account to test single sign on.</span></span> <span data-ttu-id="d41f4-110">In this tutorial, an application is deployed in the account.</span><span class="sxs-lookup"><span data-stu-id="d41f4-110">In this tutorial, an application is deployed in the account.</span></span>
> 
> 

<span data-ttu-id="d41f4-111">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d41f4-111">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="d41f4-112">Enabling the application integration for SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="d41f4-112">Enabling the application integration for SAP HANA Cloud Platform</span></span>
2. <span data-ttu-id="d41f4-113">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="d41f4-113">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="d41f4-114">Assigning a role to a user</span><span class="sxs-lookup"><span data-stu-id="d41f4-114">Assigning a role to a user</span></span>
4. <span data-ttu-id="d41f4-115">Assigning users</span><span class="sxs-lookup"><span data-stu-id="d41f4-115">Assigning users</span></span>

<span data-ttu-id="d41f4-116">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="d41f4-116">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-sap-hana-cloud-platform"></a><span data-ttu-id="d41f4-117">Enabling the application integration for SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="d41f4-117">Enabling the application integration for SAP HANA Cloud Platform</span></span>
<span data-ttu-id="d41f4-118">The objective of this section is to outline how to enable the application integration for SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="d41f4-118">The objective of this section is to outline how to enable the application integration for SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="d41f4-119">**To enable the application integration for SAP HANA Cloud Platform, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d41f4-119">**To enable the application integration for SAP HANA Cloud Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="d41f4-120">In the Azure Management Portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d41f4-120">In the Azure Management Portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="d41f4-121">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="d41f4-121">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="d41f4-122">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="d41f4-122">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d41f4-123">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="d41f4-123">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="d41f4-124">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="d41f4-124">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="d41f4-125">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="d41f4-125">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="d41f4-126">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="d41f4-126">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="d41f4-127">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="d41f4-127">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="d41f4-128">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="d41f4-128">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="d41f4-129">In the **search box**, type **SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="d41f4-129">In the **search box**, type **SAP HANA Cloud Platform**.</span></span>
   
    <span data-ttu-id="d41f4-130">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="d41f4-130">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Application Gallery")</span></span>
7. <span data-ttu-id="d41f4-131">In the results pane, select **SAP HANA Cloud Platform**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="d41f4-131">In the results pane, select **SAP HANA Cloud Platform**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="d41f4-132">![SAP Hana](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span><span class="sxs-lookup"><span data-stu-id="d41f4-132">![SAP Hana](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="d41f4-133">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="d41f4-133">Configure single sign-on</span></span>

<span data-ttu-id="d41f4-134">The objective of this section is to outline how to enable users to authenticate to SAP HANA Cloud Platform with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="d41f4-134">The objective of this section is to outline how to enable users to authenticate to SAP HANA Cloud Platform with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="d41f4-135">As part of this procedure, you are required to upload a base-64 encoded certificate to your SAP HANA Cloud Platform tenant.</span><span class="sxs-lookup"><span data-stu-id="d41f4-135">As part of this procedure, you are required to upload a base-64 encoded certificate to your SAP HANA Cloud Platform tenant.</span></span>  

<span data-ttu-id="d41f4-136">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="d41f4-136">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="d41f4-137">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d41f4-137">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="d41f4-138">In the Azure classic portal, on the **SAP HANA Cloud Platform** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="d41f4-138">In the Azure classic portal, on the **SAP HANA Cloud Platform** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="d41f4-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="d41f4-139">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="d41f4-140">On the **How would you like users to sign on to SAP HANA Cloud Platform** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d41f4-140">On the **How would you like users to sign on to SAP HANA Cloud Platform** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="d41f4-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d41f4-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="d41f4-142">In a different web browser window, sign on to the SAP HANA Cloud Platform Cockpit at https://account.\<landscape host\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span><span class="sxs-lookup"><span data-stu-id="d41f4-142">In a different web browser window, sign on to the SAP HANA Cloud Platform Cockpit at https://account.\<landscape host\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span></span>
4. <span data-ttu-id="d41f4-143">Click the **Trust** tab.</span><span class="sxs-lookup"><span data-stu-id="d41f4-143">Click the **Trust** tab.</span></span>
   
    <span data-ttu-id="d41f4-144">![Trust](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span><span class="sxs-lookup"><span data-stu-id="d41f4-144">![Trust](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span></span>
5. <span data-ttu-id="d41f4-145">In trust management section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d41f4-145">In trust management section, perform the following steps:</span></span>
   
    <span data-ttu-id="d41f4-146">![Get Metadata](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Get Metadata")</span><span class="sxs-lookup"><span data-stu-id="d41f4-146">![Get Metadata](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Get Metadata")</span></span>
   
   1. <span data-ttu-id="d41f4-147">Click the **Local Service Provider** tab.</span><span class="sxs-lookup"><span data-stu-id="d41f4-147">Click the **Local Service Provider** tab.</span></span>
   2. <span data-ttu-id="d41f4-148">To download the SAP HANA Cloud Platform metadata file, click **Get Metadata**.</span><span class="sxs-lookup"><span data-stu-id="d41f4-148">To download the SAP HANA Cloud Platform metadata file, click **Get Metadata**.</span></span>
6. <span data-ttu-id="d41f4-149">In the Azure Active classic portal, on the **Configure App URL** page, perform the following steps, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d41f4-149">In the Azure Active classic portal, on the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
    <span data-ttu-id="d41f4-150">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="d41f4-150">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configure App URL")</span></span>
   
   1. <span data-ttu-id="d41f4-151">In the **Sign On URL** textbox, type the URL used by your users to sign into your **SAP HANA Cloud Platform** application.</span><span class="sxs-lookup"><span data-stu-id="d41f4-151">In the **Sign On URL** textbox, type the URL used by your users to sign into your **SAP HANA Cloud Platform** application.</span></span> <span data-ttu-id="d41f4-152">This is the account-specific URL of a protected resource in your SAP HANA Cloud Platform application.</span><span class="sxs-lookup"><span data-stu-id="d41f4-152">This is the account-specific URL of a protected resource in your SAP HANA Cloud Platform application.</span></span> <span data-ttu-id="d41f4-153">The URL is based on the following pattern: *https://\<applicationName\>\<accountName\>.\<landscape host\>.ondemand.com/\<path\_to\_protected\_resource\>* (e.g.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span><span class="sxs-lookup"><span data-stu-id="d41f4-153">The URL is based on the following pattern: *https://\<applicationName\>\<accountName\>.\<landscape host\>.ondemand.com/\<path\_to\_protected\_resource\>* (e.g.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="d41f4-154">This is the URL in your SAP HANA Cloud Platform application that requires the user to authenticate.</span><span class="sxs-lookup"><span data-stu-id="d41f4-154">This is the URL in your SAP HANA Cloud Platform application that requires the user to authenticate.</span></span>
     > 

   2. <span data-ttu-id="d41f4-155">Open the downloaded SAP HANA Cloud Platform metadata file, and then locate the **ns3:AssertionConsumerService** tag.</span><span class="sxs-lookup"><span data-stu-id="d41f4-155">Open the downloaded SAP HANA Cloud Platform metadata file, and then locate the **ns3:AssertionConsumerService** tag.</span></span>
   3. <span data-ttu-id="d41f4-156">Copy the value of the **Location** attribute, and then paste it into the **SAP HANA Cloud Platform Reply URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="d41f4-156">Copy the value of the **Location** attribute, and then paste it into the **SAP HANA Cloud Platform Reply URL** textbox.</span></span>

7. <span data-ttu-id="d41f4-157">On the **Configure single sign-on at SAP HANA Cloud Platform** page, to download your metadata, click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d41f4-157">On the **Configure single sign-on at SAP HANA Cloud Platform** page, to download your metadata, click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="d41f4-158">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d41f4-158">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configure Single Sign-On")</span></span>
8. <span data-ttu-id="d41f4-159">On the SAP HANA Cloud Platform Cockpit, in the **Local Service Provider** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d41f4-159">On the SAP HANA Cloud Platform Cockpit, in the **Local Service Provider** section, perform the following steps:</span></span>
   
    <span data-ttu-id="d41f4-160">![Trust Management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span><span class="sxs-lookup"><span data-stu-id="d41f4-160">![Trust Management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span></span>
   
  1. <span data-ttu-id="d41f4-161">Click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="d41f4-161">Click **Edit**.</span></span>
  2. <span data-ttu-id="d41f4-162">As **Configuration Type**, select **Custom**.</span><span class="sxs-lookup"><span data-stu-id="d41f4-162">As **Configuration Type**, select **Custom**.</span></span>
  3. <span data-ttu-id="d41f4-163">As **Local Provider Name**, leave the default value.</span><span class="sxs-lookup"><span data-stu-id="d41f4-163">As **Local Provider Name**, leave the default value.</span></span>
  4. <span data-ttu-id="d41f4-164">To generate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span><span class="sxs-lookup"><span data-stu-id="d41f4-164">To generate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span></span>
  5. <span data-ttu-id="d41f4-165">As **Principal Propagation**, select **Disabled**.</span><span class="sxs-lookup"><span data-stu-id="d41f4-165">As **Principal Propagation**, select **Disabled**.</span></span>
  6. <span data-ttu-id="d41f4-166">As **Force Authentication**, select **Disabled**.</span><span class="sxs-lookup"><span data-stu-id="d41f4-166">As **Force Authentication**, select **Disabled**.</span></span>
  7. <span data-ttu-id="d41f4-167">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d41f4-167">Click **Save**.</span></span>

9. <span data-ttu-id="d41f4-168">Click the **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span><span class="sxs-lookup"><span data-stu-id="d41f4-168">Click the **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span></span>
   
    <span data-ttu-id="d41f4-169">![Trust Management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span><span class="sxs-lookup"><span data-stu-id="d41f4-169">![Trust Management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="d41f4-170">To manage the list of trusted identity providers, you need to have chosen the Custom configuration type in the Local Service Provider section.</span><span class="sxs-lookup"><span data-stu-id="d41f4-170">To manage the list of trusted identity providers, you need to have chosen the Custom configuration type in the Local Service Provider section.</span></span> <span data-ttu-id="d41f4-171">For Default configuration type, you have a non-editable and implicit trust to the SAP ID Service.</span><span class="sxs-lookup"><span data-stu-id="d41f4-171">For Default configuration type, you have a non-editable and implicit trust to the SAP ID Service.</span></span> <span data-ttu-id="d41f4-172">For None, you don't have any trust settings.</span><span class="sxs-lookup"><span data-stu-id="d41f4-172">For None, you don't have any trust settings.</span></span>
    > 
    > 

10. <span data-ttu-id="d41f4-173">Click the **General** tab, and then click **Browse** to upload the downloaded metadata file.</span><span class="sxs-lookup"><span data-stu-id="d41f4-173">Click the **General** tab, and then click **Browse** to upload the downloaded metadata file.</span></span>
    
    <span data-ttu-id="d41f4-174">![Trust Management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span><span class="sxs-lookup"><span data-stu-id="d41f4-174">![Trust Management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="d41f4-175">After uploading the metadata file, the values for **Single Sign-on URL**, **Single Logout URL** and **Signing Certificate** are populated automatically.</span><span class="sxs-lookup"><span data-stu-id="d41f4-175">After uploading the metadata file, the values for **Single Sign-on URL**, **Single Logout URL** and **Signing Certificate** are populated automatically.</span></span>
    > 
    > 

11. <span data-ttu-id="d41f4-176">Click the **Attributes** tab.</span><span class="sxs-lookup"><span data-stu-id="d41f4-176">Click the **Attributes** tab.</span></span>
12. <span data-ttu-id="d41f4-177">On the **Attributes** tab, perform the following step:</span><span class="sxs-lookup"><span data-stu-id="d41f4-177">On the **Attributes** tab, perform the following step:</span></span>
    
    <span data-ttu-id="d41f4-178">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="d41f4-178">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributes")</span></span> 
  * <span data-ttu-id="d41f4-179">Click **Add Assertion-Based Attribute**, and then add the following assertion-based attributes:</span><span class="sxs-lookup"><span data-stu-id="d41f4-179">Click **Add Assertion-Based Attribute**, and then add the following assertion-based attributes:</span></span>
       
    | <span data-ttu-id="d41f4-180">Assertion Attribute</span><span class="sxs-lookup"><span data-stu-id="d41f4-180">Assertion Attribute</span></span> | <span data-ttu-id="d41f4-181">Principal Attribute</span><span class="sxs-lookup"><span data-stu-id="d41f4-181">Principal Attribute</span></span> |
    | --- | --- |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname |<span data-ttu-id="d41f4-182">firstname</span><span class="sxs-lookup"><span data-stu-id="d41f4-182">firstname</span></span> |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname |<span data-ttu-id="d41f4-183">lastname</span><span class="sxs-lookup"><span data-stu-id="d41f4-183">lastname</span></span> |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress |<span data-ttu-id="d41f4-184">email</span><span class="sxs-lookup"><span data-stu-id="d41f4-184">email</span></span> 
   
     >[!NOTE]
     ><span data-ttu-id="d41f4-185">The configuration of the Attributes depends on how the application(s) on HCP are developed, i.e. which attribute(s) they expect in the SAML response and under which name (Principal Attribute) they access this attribute in the code.</span><span class="sxs-lookup"><span data-stu-id="d41f4-185">The configuration of the Attributes depends on how the application(s) on HCP are developed, i.e. which attribute(s) they expect in the SAML response and under which name (Principal Attribute) they access this attribute in the code.</span></span>
     > 
     >  

    1.  <span data-ttu-id="d41f4-186">The **Default Attribute** in the screenshot is just for illustration purposes.</span><span class="sxs-lookup"><span data-stu-id="d41f4-186">The **Default Attribute** in the screenshot is just for illustration purposes.</span></span> <span data-ttu-id="d41f4-187">It is not required to make the scenario work.</span><span class="sxs-lookup"><span data-stu-id="d41f4-187">It is not required to make the scenario work.</span></span>   
    2.  <span data-ttu-id="d41f4-188">The names and values for **Principal Attribute** shown in the screenshot depend on how the application is developed.</span><span class="sxs-lookup"><span data-stu-id="d41f4-188">The names and values for **Principal Attribute** shown in the screenshot depend on how the application is developed.</span></span> <span data-ttu-id="d41f4-189">It is possible that your application requires different mappings.</span><span class="sxs-lookup"><span data-stu-id="d41f4-189">It is possible that your application requires different mappings.</span></span>
     
13. <span data-ttu-id="d41f4-190">In the Azure classic portal, on the **Configure single sign-on at SAP HANA Cloud Platform** dialogue page, select the single sign-on configuration confirmation, and then click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="d41f4-190">In the Azure classic portal, on the **Configure single sign-on at SAP HANA Cloud Platform** dialogue page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="d41f4-191">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d41f4-191">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configure Single Sign-On")</span></span>

###<a name="assertion-based-groups"></a><span data-ttu-id="d41f4-192">Assertion-based groups</span><span class="sxs-lookup"><span data-stu-id="d41f4-192">Assertion-based groups</span></span>
<span data-ttu-id="d41f4-193">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span><span class="sxs-lookup"><span data-stu-id="d41f4-193">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span></span>

<span data-ttu-id="d41f4-194">Using groups on SAP HANA Cloud Platform allows you to dynamically assign one or more users to one or more roles in your SAP HANA Cloud Platform applications, determined by values of attributes in the SAML 2.0 assertion.</span><span class="sxs-lookup"><span data-stu-id="d41f4-194">Using groups on SAP HANA Cloud Platform allows you to dynamically assign one or more users to one or more roles in your SAP HANA Cloud Platform applications, determined by values of attributes in the SAML 2.0 assertion.</span></span> 

<span data-ttu-id="d41f4-195">For example, if the assertion contains the attribute "*contract=temporary*", you may want all affected users to be added to the group "*TEMPORARY*".</span><span class="sxs-lookup"><span data-stu-id="d41f4-195">For example, if the assertion contains the attribute "*contract=temporary*", you may want all affected users to be added to the group "*TEMPORARY*".</span></span> <span data-ttu-id="d41f4-196">The group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP HANA Cloud Platform account.</span><span class="sxs-lookup"><span data-stu-id="d41f4-196">The group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP HANA Cloud Platform account.</span></span>
 
<span data-ttu-id="d41f4-197">Use assertion-based groups when you want to simultaneously assign many users to one or more roles of applications in your SAP HANA Cloud Platform account.</span><span class="sxs-lookup"><span data-stu-id="d41f4-197">Use assertion-based groups when you want to simultaneously assign many users to one or more roles of applications in your SAP HANA Cloud Platform account.</span></span> <span data-ttu-id="d41f4-198">If you want to assign only a single or small number of users to specific roles, we recommend assigning them directly in the “**Authorizations**” tab of the SAP HANA Cloud Platform cockpit.</span><span class="sxs-lookup"><span data-stu-id="d41f4-198">If you want to assign only a single or small number of users to specific roles, we recommend assigning them directly in the “**Authorizations**” tab of the SAP HANA Cloud Platform cockpit.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="d41f4-199">Assign a role to a user</span><span class="sxs-lookup"><span data-stu-id="d41f4-199">Assign a role to a user</span></span>
<span data-ttu-id="d41f4-200">In order to enable Azure AD users to log into SAP HANA Cloud Platform, you must assign roles in the SAP HANA Cloud Platform to them.</span><span class="sxs-lookup"><span data-stu-id="d41f4-200">In order to enable Azure AD users to log into SAP HANA Cloud Platform, you must assign roles in the SAP HANA Cloud Platform to them.</span></span>

<span data-ttu-id="d41f4-201">**To assign a role to a user, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d41f4-201">**To assign a role to a user, perform the following steps:**</span></span>

1. <span data-ttu-id="d41f4-202">Log in to your **SAP HANA Cloud Platform** cockpit.</span><span class="sxs-lookup"><span data-stu-id="d41f4-202">Log in to your **SAP HANA Cloud Platform** cockpit.</span></span>
2. <span data-ttu-id="d41f4-203">Perform the following:</span><span class="sxs-lookup"><span data-stu-id="d41f4-203">Perform the following:</span></span>
   
   <span data-ttu-id="d41f4-204">![Authorizations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Authorizations")</span><span class="sxs-lookup"><span data-stu-id="d41f4-204">![Authorizations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Authorizations")</span></span>
   
  1. <span data-ttu-id="d41f4-205">Click **Authorization**.</span><span class="sxs-lookup"><span data-stu-id="d41f4-205">Click **Authorization**.</span></span>
  2. <span data-ttu-id="d41f4-206">Click the **Users** tab.</span><span class="sxs-lookup"><span data-stu-id="d41f4-206">Click the **Users** tab.</span></span>
  3. <span data-ttu-id="d41f4-207">In the **User** textbox, type the user’s email address.</span><span class="sxs-lookup"><span data-stu-id="d41f4-207">In the **User** textbox, type the user’s email address.</span></span>
  4. <span data-ttu-id="d41f4-208">Click **Assign** to assign the user to a role.</span><span class="sxs-lookup"><span data-stu-id="d41f4-208">Click **Assign** to assign the user to a role.</span></span>
  5. <span data-ttu-id="d41f4-209">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d41f4-209">Click **Save**.</span></span>

## <a name="assign-users"></a><span data-ttu-id="d41f4-210">Assign users</span><span class="sxs-lookup"><span data-stu-id="d41f4-210">Assign users</span></span>
<span data-ttu-id="d41f4-211">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="d41f4-211">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="d41f4-212">**To assign users to SAP HANA Cloud Platform, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d41f4-212">**To assign users to SAP HANA Cloud Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="d41f4-213">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="d41f4-213">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="d41f4-214">On the **SAP HANA Cloud Platform** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="d41f4-214">On the **SAP HANA Cloud Platform** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="d41f4-215">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="d41f4-215">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assign Users")</span></span>
3. <span data-ttu-id="d41f4-216">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="d41f4-216">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="d41f4-217">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="d41f4-217">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="d41f4-218">If you want to test your SSO settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d41f4-218">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="d41f4-219">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d41f4-219">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>






















