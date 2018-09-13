---
title: 'Tutorial: Azure Active Directory integration with Benefitsolver | Microsoft Docs'
description: Learn how to use Benefitsolver with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: ddbac6812eafc452193107cdcd2ac2671c970fd0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551976"
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="39a73-103">Tutorial: Azure Active Directory integration with Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="39a73-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="39a73-104">The objective of this tutorial is to show the integration of Azure and Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="39a73-104">The objective of this tutorial is to show the integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="39a73-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="39a73-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="39a73-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="39a73-106">A valid Azure subscription</span></span>
* <span data-ttu-id="39a73-107">A Benefitsolver single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="39a73-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="39a73-108">After completing this tutorial, the Azure AD users you have assigned to Benefitsolver will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="39a73-108">After completing this tutorial, the Azure AD users you have assigned to Benefitsolver will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="39a73-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="39a73-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="39a73-110">Enabling the application integration for Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="39a73-110">Enabling the application integration for Benefitsolver</span></span>
2. <span data-ttu-id="39a73-111">Configuring single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="39a73-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="39a73-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="39a73-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="39a73-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="39a73-113">Assigning users</span></span>

<span data-ttu-id="39a73-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="39a73-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-benefitsolver"></a><span data-ttu-id="39a73-115">Enabling the application integration for Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="39a73-115">Enabling the application integration for Benefitsolver</span></span>
<span data-ttu-id="39a73-116">The objective of this section is to outline how to enable the application integration for Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="39a73-116">The objective of this section is to outline how to enable the application integration for Benefitsolver.</span></span>

### <a name="to-enable-the-application-integration-for-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="39a73-117">To enable the application integration for Benefitsolver, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="39a73-117">To enable the application integration for Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="39a73-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="39a73-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="39a73-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="39a73-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="39a73-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="39a73-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="39a73-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="39a73-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="39a73-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="39a73-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="39a73-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="39a73-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="39a73-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="39a73-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="39a73-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="39a73-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="39a73-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="39a73-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="39a73-127">In the **search box**, type **Benefitsolver**.</span><span class="sxs-lookup"><span data-stu-id="39a73-127">In the **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="39a73-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="39a73-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="39a73-129">In the results pane, select **Benefitsolver**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="39a73-129">In the results pane, select **Benefitsolver**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="39a73-130">![Benefitssolver](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="39a73-130">![Benefitssolver](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="39a73-131">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="39a73-131">Configure single sign-on</span></span>

<span data-ttu-id="39a73-132">The objective of this section is to outline how to enable users to authenticate to Benefitsolver with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="39a73-132">The objective of this section is to outline how to enable users to authenticate to Benefitsolver with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="39a73-133">Your Benefitsolver application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span><span class="sxs-lookup"><span data-stu-id="39a73-133">Your Benefitsolver application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> 

<span data-ttu-id="39a73-134">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="39a73-134">The following screenshot shows an example for this.</span></span>

<span data-ttu-id="39a73-135">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="39a73-135">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="39a73-136">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="39a73-136">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="39a73-137">In the Azure classic portal, on the **Benefitsolver** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="39a73-137">In the Azure classic portal, on the **Benefitsolver** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="39a73-138">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="39a73-138">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="39a73-139">On the **How would you like users to sign on to Benefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="39a73-139">On the **How would you like users to sign on to Benefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="39a73-140">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="39a73-140">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="39a73-141">On the **Configure App Settings** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="39a73-141">On the **Configure App Settings** page, perform the following steps:</span></span>
   
   <span data-ttu-id="39a73-142">![Configure App Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span><span class="sxs-lookup"><span data-stu-id="39a73-142">![Configure App Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="39a73-143">In the **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span><span class="sxs-lookup"><span data-stu-id="39a73-143">In the **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="39a73-144">In the **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span><span class="sxs-lookup"><span data-stu-id="39a73-144">In the **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="39a73-145">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="39a73-145">Click **Next**.</span></span>
4. <span data-ttu-id="39a73-146">On the **Configure single sign-on at Benefitsolver** page, to download your metadata, click **Download metadata**, and then save the metadata file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="39a73-146">On the **Configure single sign-on at Benefitsolver** page, to download your metadata, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="39a73-147">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="39a73-147">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="39a73-148">Send the downloaded metadata file to your Benefitsolver support team.</span><span class="sxs-lookup"><span data-stu-id="39a73-148">Send the downloaded metadata file to your Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="39a73-149">Your Benefitsolver support team has to do the actual SSO configuration.</span><span class="sxs-lookup"><span data-stu-id="39a73-149">Your Benefitsolver support team has to do the actual SSO configuration.</span></span> <span data-ttu-id="39a73-150">You will get a notification when SSO has been enabled for your subscription.</span><span class="sxs-lookup"><span data-stu-id="39a73-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="39a73-151">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="39a73-151">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="39a73-152">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="39a73-152">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="39a73-153">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span><span class="sxs-lookup"><span data-stu-id="39a73-153">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="39a73-154">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="39a73-154">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="39a73-155">To add the required attribute mappings, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="39a73-155">To add the required attribute mappings, perform the following steps:</span></span>
   
   <span data-ttu-id="39a73-156">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="39a73-156">![Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="39a73-157">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="39a73-157">Attribute Name</span></span> | <span data-ttu-id="39a73-158">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="39a73-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="39a73-159">ClientID</span><span class="sxs-lookup"><span data-stu-id="39a73-159">ClientID</span></span> |<span data-ttu-id="39a73-160">You need to get this value from your Benefitsolver support team.</span><span class="sxs-lookup"><span data-stu-id="39a73-160">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="39a73-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="39a73-161">ClientKey</span></span> |<span data-ttu-id="39a73-162">You need to get this value from your Benefitsolver support team.</span><span class="sxs-lookup"><span data-stu-id="39a73-162">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="39a73-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="39a73-163">LogoutURL</span></span> |<span data-ttu-id="39a73-164">You need to get this value from your Benefitsolver support team.</span><span class="sxs-lookup"><span data-stu-id="39a73-164">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="39a73-165">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="39a73-165">EmployeeID</span></span> |<span data-ttu-id="39a73-166">You need to get this value from your Benefitsolver support team.</span><span class="sxs-lookup"><span data-stu-id="39a73-166">You need to get this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="39a73-167">For each data row in the table above, click **add user attribute**.</span><span class="sxs-lookup"><span data-stu-id="39a73-167">For each data row in the table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="39a73-168">In the **Attribute Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="39a73-168">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
   3. <span data-ttu-id="39a73-169">In the **Attribute Value** textbox, select the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="39a73-169">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
   4. <span data-ttu-id="39a73-170">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="39a73-170">Click **Complete**.</span></span>
9. <span data-ttu-id="39a73-171">Click **Apply Changes**.</span><span class="sxs-lookup"><span data-stu-id="39a73-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="39a73-172">Configure user provisioning</span><span class="sxs-lookup"><span data-stu-id="39a73-172">Configure user provisioning</span></span>
<span data-ttu-id="39a73-173">In order to enable Azure AD users to log into Benefitsolver, they must be provisioned into Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="39a73-173">In order to enable Azure AD users to log into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="39a73-174">In the case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span><span class="sxs-lookup"><span data-stu-id="39a73-174">In the case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="39a73-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="39a73-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver to provision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="39a73-176">Assigning users</span><span class="sxs-lookup"><span data-stu-id="39a73-176">Assigning users</span></span>
<span data-ttu-id="39a73-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="39a73-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="39a73-178">To assign users to Benefitsolver, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="39a73-178">To assign users to Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="39a73-179">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="39a73-179">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="39a73-180">On the \*\*Benefitsolver \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="39a73-180">On the \*\*Benefitsolver \*\*application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="39a73-181">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="39a73-181">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="39a73-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="39a73-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="39a73-183">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="39a73-183">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="39a73-184">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="39a73-184">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="39a73-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="39a73-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


















