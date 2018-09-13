---
title: 'Tutorial: Azure Active Directory integration with ShiftPlanning | Microsoft Docs'
description: Learn how to use ShiftPlanning with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/22/2017
ms.author: jeedes
ms.openlocfilehash: 50da89db9e7d3d0ed0ed3d054a767af55a087b7f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564442"
---
# <a name="tutorial-azure-active-directory-integration-with-shiftplanning"></a><span data-ttu-id="110f8-103">Tutorial: Azure Active Directory integration with ShiftPlanning</span><span class="sxs-lookup"><span data-stu-id="110f8-103">Tutorial: Azure Active Directory integration with ShiftPlanning</span></span>
<span data-ttu-id="110f8-104">The objective of this tutorial is to show the integration of Azure and ShiftPlanning.</span><span class="sxs-lookup"><span data-stu-id="110f8-104">The objective of this tutorial is to show the integration of Azure and ShiftPlanning.</span></span>

<span data-ttu-id="110f8-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="110f8-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="110f8-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="110f8-106">A valid Azure subscription</span></span>
* <span data-ttu-id="110f8-107">A ShiftPlanning single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="110f8-107">A ShiftPlanning single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="110f8-108">After completing this tutorial, the Azure AD users you have assigned to ShiftPlanning will be able to single sign into the application at your ShiftPlanning company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="110f8-108">After completing this tutorial, the Azure AD users you have assigned to ShiftPlanning will be able to single sign into the application at your ShiftPlanning company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="110f8-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="110f8-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="110f8-110">Enabling the application integration for ShiftPlanning</span><span class="sxs-lookup"><span data-stu-id="110f8-110">Enabling the application integration for ShiftPlanning</span></span>
2. <span data-ttu-id="110f8-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="110f8-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="110f8-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="110f8-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="110f8-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="110f8-113">Assigning users</span></span>

<span data-ttu-id="110f8-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786612.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="110f8-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786612.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-shiftplanning"></a><span data-ttu-id="110f8-115">Enable the application integration for ShiftPlanning</span><span class="sxs-lookup"><span data-stu-id="110f8-115">Enable the application integration for ShiftPlanning</span></span>
<span data-ttu-id="110f8-116">The objective of this section is to outline how to enable the application integration for ShiftPlanning.</span><span class="sxs-lookup"><span data-stu-id="110f8-116">The objective of this section is to outline how to enable the application integration for ShiftPlanning.</span></span>

<span data-ttu-id="110f8-117">**To enable the application integration for ShiftPlanning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="110f8-117">**To enable the application integration for ShiftPlanning, perform the following steps:**</span></span>

1. <span data-ttu-id="110f8-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="110f8-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="110f8-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="110f8-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="110f8-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="110f8-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="110f8-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="110f8-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="110f8-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="110f8-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="110f8-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="110f8-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="110f8-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="110f8-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="110f8-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="110f8-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="110f8-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="110f8-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="110f8-127">In the **search box**, type **ShiftPlanning**.</span><span class="sxs-lookup"><span data-stu-id="110f8-127">In the **search box**, type **ShiftPlanning**.</span></span>
   
    <span data-ttu-id="110f8-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786613.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="110f8-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786613.png "Application Gallery")</span></span>

7. <span data-ttu-id="110f8-129">In the results pane, select **ShiftPlanning**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="110f8-129">In the results pane, select **ShiftPlanning**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="110f8-130">![ShiftPlanning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786614.png "ShiftPlanning")</span><span class="sxs-lookup"><span data-stu-id="110f8-130">![ShiftPlanning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786614.png "ShiftPlanning")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="110f8-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="110f8-131">Configure single sign-on</span></span>

<span data-ttu-id="110f8-132">The objective of this section is to outline how to enable users to authenticate to ShiftPlanning with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="110f8-132">The objective of this section is to outline how to enable users to authenticate to ShiftPlanning with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="110f8-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="110f8-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span>  

<span data-ttu-id="110f8-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="110f8-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="110f8-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="110f8-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="110f8-136">In the Azure classic portal, on the **ShiftPlanning** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="110f8-136">In the Azure classic portal, on the **ShiftPlanning** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="110f8-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786615.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="110f8-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786615.png "Configure Single Sign-On")</span></span>

2. <span data-ttu-id="110f8-138">On the **How would you like users to sign on to ShiftPlanning** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="110f8-138">On the **How would you like users to sign on to ShiftPlanning** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="110f8-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786616.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="110f8-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786616.png "Configure Single Sign-On")</span></span>

3. <span data-ttu-id="110f8-140">On the **Configure App URL** page, in the **ShiftPlanning Sign On URL** textbox, type your URL using the following pattern "*https://company.shiftplanning.com/includes/saml/*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="110f8-140">On the **Configure App URL** page, in the **ShiftPlanning Sign On URL** textbox, type your URL using the following pattern "*https://company.shiftplanning.com/includes/saml/*", and then click **Next**.</span></span>
   
    <span data-ttu-id="110f8-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786617.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="110f8-141">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786617.png "Configure App URL")</span></span>

4. <span data-ttu-id="110f8-142">On the **Configure single sign-on at ShiftPlanning** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="110f8-142">On the **Configure single sign-on at ShiftPlanning** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
    <span data-ttu-id="110f8-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786618.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="110f8-143">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786618.png "Configure Single Sign-On")</span></span>

5. <span data-ttu-id="110f8-144">In a different web browser window, log into your **ShiftPlanning** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="110f8-144">In a different web browser window, log into your **ShiftPlanning** company site as an administrator.</span></span>
6. <span data-ttu-id="110f8-145">In the menu on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="110f8-145">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="110f8-146">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786619.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="110f8-146">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786619.png "Admin")</span></span>

7. <span data-ttu-id="110f8-147">Under **Integration**, click **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="110f8-147">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="110f8-148">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786620.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="110f8-148">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786620.png "Single Sign-On")</span></span>

8. <span data-ttu-id="110f8-149">In the **Single Sign-On** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="110f8-149">In the **Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="110f8-150">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786905.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="110f8-150">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786905.png "Single Sign-On")</span></span>
   
   1. <span data-ttu-id="110f8-151">Select **SAML Enabled**.</span><span class="sxs-lookup"><span data-stu-id="110f8-151">Select **SAML Enabled**.</span></span>
   2. <span data-ttu-id="110f8-152">Select **Allow Password Login**.</span><span class="sxs-lookup"><span data-stu-id="110f8-152">Select **Allow Password Login**.</span></span>
   3. <span data-ttu-id="110f8-153">In the Azure classic portal, on the **Configure single sign-on at ShiftPlanning** dialog page, copy the **Remote Login URL** value, and then paste it into the **SAML Issuer URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="110f8-153">In the Azure classic portal, on the **Configure single sign-on at ShiftPlanning** dialog page, copy the **Remote Login URL** value, and then paste it into the **SAML Issuer URL** textbox.</span></span>
   4. <span data-ttu-id="110f8-154">In the Azure classic portal, on the **Configure single sign-on at ShiftPlanning** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Remote Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="110f8-154">In the Azure classic portal, on the **Configure single sign-on at ShiftPlanning** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Remote Logout URL** textbox.</span></span>
   5. <span data-ttu-id="110f8-155">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="110f8-155">Create a **base-64 encoded** file from your downloaded certificate.</span></span>  
       
     >[!TIP]
     ><span data-ttu-id="110f8-156">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="110f8-156">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
     > 
     > 

   6. <span data-ttu-id="110f8-157">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="110f8-157">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
   7. <span data-ttu-id="110f8-158">Click **Save Settings**.</span><span class="sxs-lookup"><span data-stu-id="110f8-158">Click **Save Settings**.</span></span>

9. <span data-ttu-id="110f8-159">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="110f8-159">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="110f8-160">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786621.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="110f8-160">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786621.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="110f8-161">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="110f8-161">Configure user provisioning</span></span>

<span data-ttu-id="110f8-162">In order to enable Azure AD users to log into ShiftPlanning, they must be provisioned into ShiftPlanning.</span><span class="sxs-lookup"><span data-stu-id="110f8-162">In order to enable Azure AD users to log into ShiftPlanning, they must be provisioned into ShiftPlanning.</span></span>  

<span data-ttu-id="110f8-163">In the case of ShiftPlanning, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="110f8-163">In the case of ShiftPlanning, provisioning is a manual task.</span></span>

<span data-ttu-id="110f8-164">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="110f8-164">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="110f8-165">Log in to your **ShiftPlanning** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="110f8-165">Log in to your **ShiftPlanning** company site as an administrator.</span></span>
2. <span data-ttu-id="110f8-166">Click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="110f8-166">Click **Admin**.</span></span>
   
    <span data-ttu-id="110f8-167">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786619.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="110f8-167">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786619.png "Admin")</span></span>
3. <span data-ttu-id="110f8-168">Click **Staff**.</span><span class="sxs-lookup"><span data-stu-id="110f8-168">Click **Staff**.</span></span>
   
    <span data-ttu-id="110f8-169">![Staff](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786623.png "Staff")</span><span class="sxs-lookup"><span data-stu-id="110f8-169">![Staff](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786623.png "Staff")</span></span>
4. <span data-ttu-id="110f8-170">Under **Actions**, click **Add Employee**.</span><span class="sxs-lookup"><span data-stu-id="110f8-170">Under **Actions**, click **Add Employee**.</span></span>
   
    <span data-ttu-id="110f8-171">![Add Employees](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786624.png "Add Employees")</span><span class="sxs-lookup"><span data-stu-id="110f8-171">![Add Employees](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786624.png "Add Employees")</span></span>
5. <span data-ttu-id="110f8-172">In the **Add Employees** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="110f8-172">In the **Add Employees** section, perform the following steps:</span></span>
   
    <span data-ttu-id="110f8-173">![Save Employees](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786625.png "Save Employees")</span><span class="sxs-lookup"><span data-stu-id="110f8-173">![Save Employees](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786625.png "Save Employees")</span></span>
   
   1. <span data-ttu-id="110f8-174">Type the **First Name**, **Last Name** and **Email** of a valid AAD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="110f8-174">Type the **First Name**, **Last Name** and **Email** of a valid AAD account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="110f8-175">Click **Save Employees**.</span><span class="sxs-lookup"><span data-stu-id="110f8-175">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="110f8-176">You can use any other ShiftPlanning user account creation tools or APIs provided by ShiftPlanning to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="110f8-176">You can use any other ShiftPlanning user account creation tools or APIs provided by ShiftPlanning to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="110f8-177">Assign users</span><span class="sxs-lookup"><span data-stu-id="110f8-177">Assign users</span></span>
<span data-ttu-id="110f8-178">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="110f8-178">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="110f8-179">**To assign users to ShiftPlanning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="110f8-179">**To assign users to ShiftPlanning, perform the following steps:**</span></span>

1. <span data-ttu-id="110f8-180">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="110f8-180">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="110f8-181">On the **ShiftPlanning** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="110f8-181">On the **ShiftPlanning** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="110f8-182">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786626.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="110f8-182">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC786626.png "Assign Users")</span></span>

3. <span data-ttu-id="110f8-183">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="110f8-183">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="110f8-184">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="110f8-184">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-shiftplanning-tutorial/IC767830.png "Yes")</span></span>
 
<span data-ttu-id="110f8-185">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="110f8-185">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="110f8-186">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="110f8-186">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>






















