---
title: 'Tutorial: Azure Active Directory integration with DocuSign | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and DocuSign.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0398dd08ed688ed9b9e0828c878f06273d3ffe97
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550282"
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="b09b8-103">Tutorial: Azure Active Directory integration with DocuSign</span><span class="sxs-lookup"><span data-stu-id="b09b8-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>
<span data-ttu-id="b09b8-104">The objective of this tutorial is to show the integration of Azure and DocuSign.</span><span class="sxs-lookup"><span data-stu-id="b09b8-104">The objective of this tutorial is to show the integration of Azure and DocuSign.</span></span>
<span data-ttu-id="b09b8-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="b09b8-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="b09b8-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="b09b8-106">A valid Azure subscription</span></span>
* <span data-ttu-id="b09b8-107">A tenant in DocuSign</span><span class="sxs-lookup"><span data-stu-id="b09b8-107">A tenant in DocuSign</span></span>

<span data-ttu-id="b09b8-108">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b09b8-108">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. [<span data-ttu-id="b09b8-109">Enabling the application integration for DocuSign</span><span class="sxs-lookup"><span data-stu-id="b09b8-109">Enabling the application integration for DocuSign</span></span>](#enabling-the-application-integration-for-docusign) 
2. [<span data-ttu-id="b09b8-110">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="b09b8-110">Configuring single sign-on</span></span>](#configuring-single-sign-on) 
3. [<span data-ttu-id="b09b8-111">Configuring account provisioning</span><span class="sxs-lookup"><span data-stu-id="b09b8-111">Configuring account provisioning</span></span>](#configuring-account-provisioning) 
4. [<span data-ttu-id="b09b8-112">Assigning users</span><span class="sxs-lookup"><span data-stu-id="b09b8-112">Assigning users</span></span>](#assigning-users) 
   
![Configuring single sign-on][0]

## <a name="enabling-the-application-integration-for-docusign"></a><span data-ttu-id="b09b8-114">Enabling the application integration for DocuSign</span><span class="sxs-lookup"><span data-stu-id="b09b8-114">Enabling the application integration for DocuSign</span></span>
<span data-ttu-id="b09b8-115">The objective of this section is to outline how to enable the application integration for DocuSign.</span><span class="sxs-lookup"><span data-stu-id="b09b8-115">The objective of this section is to outline how to enable the application integration for DocuSign.</span></span>

### <a name="to-enable-the-application-integration-for-docusign-perform-the-following-steps"></a><span data-ttu-id="b09b8-116">To enable the application integration for DocuSign, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b09b8-116">To enable the application integration for DocuSign, perform the following steps:</span></span>
1. <span data-ttu-id="b09b8-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Configuring single sign-on][1]
2. <span data-ttu-id="b09b8-119">From the Directory list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="b09b8-119">From the Directory list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="b09b8-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="b09b8-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Configuring single sign-on][2]
4. <span data-ttu-id="b09b8-122">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="b09b8-122">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="b09b8-124">On the What do you want to do dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-124">On the What do you want to do dialog, click **Add an application from the gallery**.</span></span>
   
    ![Configuring single sign-on][4]
6. <span data-ttu-id="b09b8-126">In the search box, type **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-126">In the search box, type **DocuSign**.</span></span>
   
    ![Configuring single sign-on][5]
7. <span data-ttu-id="b09b8-128">In the results pane, select **DocuSign**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="b09b8-128">In the results pane, select **DocuSign**, and then click **Complete** to add the application.</span></span>
   
    ![Configuring single sign-on][6]

## <a name="configuring-single-sign-on"></a><span data-ttu-id="b09b8-130">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="b09b8-130">Configuring single sign-on</span></span>
<span data-ttu-id="b09b8-131">The objective of this section is to outline how to enable users to authenticate to DocuSign with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="b09b8-131">The objective of this section is to outline how to enable users to authenticate to DocuSign with their account in Azure AD using federation based on the SAML protocol.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="b09b8-132">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b09b8-132">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="b09b8-133">In the Azure classic portal, on the **DocuSign application integration** page, click **Configure single sign-on** to open the Configure Single Sign On dialog.</span><span class="sxs-lookup"><span data-stu-id="b09b8-133">In the Azure classic portal, on the **DocuSign application integration** page, click **Configure single sign-on** to open the Configure Single Sign On dialog.</span></span>
   
    ![Configuring single sign-on][7]
2. <span data-ttu-id="b09b8-135">On the **How would you like users to sign on to DocuSign** page, select **Microsoft Azure AD Single Sign-On**, and then click Next.</span><span class="sxs-lookup"><span data-stu-id="b09b8-135">On the **How would you like users to sign on to DocuSign** page, select **Microsoft Azure AD Single Sign-On**, and then click Next.</span></span>
   
    ![Configuring single sign-on][8]
3. <span data-ttu-id="b09b8-137">On the **Configure App Settings** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b09b8-137">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    ![Configuring single sign-on][61]
   
    <span data-ttu-id="b09b8-139">a.</span><span class="sxs-lookup"><span data-stu-id="b09b8-139">a.</span></span> <span data-ttu-id="b09b8-140">In the **Sign on URL** textbox, type `https://account.docusign.com/*`.</span><span class="sxs-lookup"><span data-stu-id="b09b8-140">In the **Sign on URL** textbox, type `https://account.docusign.com/*`.</span></span>  
   
    <span data-ttu-id="b09b8-141">b.</span><span class="sxs-lookup"><span data-stu-id="b09b8-141">b.</span></span> <span data-ttu-id="b09b8-142">In the **Identifier** textbox, type `https://account.docusign.com/*`.</span><span class="sxs-lookup"><span data-stu-id="b09b8-142">In the **Identifier** textbox, type `https://account.docusign.com/*`.</span></span>  
   
    <span data-ttu-id="b09b8-143">c.</span><span class="sxs-lookup"><span data-stu-id="b09b8-143">c.</span></span> <span data-ttu-id="b09b8-144">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-144">Click **Next**.</span></span> 

    > [!TIP] 
    > <span data-ttu-id="b09b8-145">The Sign On URL and the Identifier values are only placeholders.</span><span class="sxs-lookup"><span data-stu-id="b09b8-145">The Sign On URL and the Identifier values are only placeholders.</span></span> <span data-ttu-id="b09b8-146">Instructions for how to retrieve the actual values for your environment are covered later in this topic.</span><span class="sxs-lookup"><span data-stu-id="b09b8-146">Instructions for how to retrieve the actual values for your environment are covered later in this topic.</span></span>


1. <span data-ttu-id="b09b8-147">On the **Configure single sign-on at DocuSign** page, click **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="b09b8-147">On the **Configure single sign-on at DocuSign** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![Configuring single sign-on][10]
2. <span data-ttu-id="b09b8-149">In a different web browser window, log into your **DocuSign admin portal** as an administrator.</span><span class="sxs-lookup"><span data-stu-id="b09b8-149">In a different web browser window, log into your **DocuSign admin portal** as an administrator.</span></span>
3. <span data-ttu-id="b09b8-150">In the navigation menu on the left, click **Domains**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-150">In the navigation menu on the left, click **Domains**.</span></span>
   
    ![Configuring single sign-on][51]
4. <span data-ttu-id="b09b8-152">On the right pane, click **Claim Domain**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-152">On the right pane, click **Claim Domain**.</span></span>
   
    ![Configuring single sign-on][52]
5. <span data-ttu-id="b09b8-154">On the **Claim a domain** dialog, in the **Domain Name** textbox, type your company domain, and then click **Claim**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-154">On the **Claim a domain** dialog, in the **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="b09b8-155">Make sure that you verify the domain and the status is active.</span><span class="sxs-lookup"><span data-stu-id="b09b8-155">Make sure that you verify the domain and the status is active.</span></span>
   
    ![Configuring single sign-on][53]
6. <span data-ttu-id="b09b8-157">In menu on the left side, click **Identity Providers**</span><span class="sxs-lookup"><span data-stu-id="b09b8-157">In menu on the left side, click **Identity Providers**</span></span>  
   
    ![Configuring single sign-on][54]
7. <span data-ttu-id="b09b8-159">In the right pane, click **Add Identity Provider**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-159">In the right pane, click **Add Identity Provider**.</span></span> 
   
    ![Configuring single sign-on][55]
8. <span data-ttu-id="b09b8-161">On the **Identity Provider Settings** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b09b8-161">On the **Identity Provider Settings** page, perform the following steps:</span></span>
   
    ![Configuring single sign-on][56]

    <span data-ttu-id="b09b8-163">a.</span><span class="sxs-lookup"><span data-stu-id="b09b8-163">a.</span></span> <span data-ttu-id="b09b8-164">In the **Name** textbox, type a unique name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="b09b8-164">In the **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="b09b8-165">Please do not use spaces.</span><span class="sxs-lookup"><span data-stu-id="b09b8-165">Please do not use spaces.</span></span>

    <span data-ttu-id="b09b8-166">b.</span><span class="sxs-lookup"><span data-stu-id="b09b8-166">b.</span></span> <span data-ttu-id="b09b8-167">In the Azure classic portal, copy the Issuer URL, and then paste it into the **Identity Provider Issuer** textbox.</span><span class="sxs-lookup"><span data-stu-id="b09b8-167">In the Azure classic portal, copy the Issuer URL, and then paste it into the **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="b09b8-168">c.</span><span class="sxs-lookup"><span data-stu-id="b09b8-168">c.</span></span> <span data-ttu-id="b09b8-169">In the Azure classic portal, copy the **Remote Login URL**, and then paste it into the **Identity Provider Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="b09b8-169">In the Azure classic portal, copy the **Remote Login URL**, and then paste it into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="b09b8-170">d.</span><span class="sxs-lookup"><span data-stu-id="b09b8-170">d.</span></span> <span data-ttu-id="b09b8-171">In the Azure classic portal, copy the **Remote Logout URL**, and then paste it into the **Identity Provider Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="b09b8-171">In the Azure classic portal, copy the **Remote Logout URL**, and then paste it into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="b09b8-172">e.</span><span class="sxs-lookup"><span data-stu-id="b09b8-172">e.</span></span> <span data-ttu-id="b09b8-173">Select **Sign AuthN Request**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-173">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="b09b8-174">f.</span><span class="sxs-lookup"><span data-stu-id="b09b8-174">f.</span></span> <span data-ttu-id="b09b8-175">As **Send AuthN request by**, select **POST**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-175">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="b09b8-176">g.</span><span class="sxs-lookup"><span data-stu-id="b09b8-176">g.</span></span> <span data-ttu-id="b09b8-177">As **Send logout request by**, select **POST**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-177">As **Send logout request by**, select **POST**.</span></span> 


1. <span data-ttu-id="b09b8-178">In the **Custom Attribute Mapping** section, choose the field you want to map with Azure AD Claim.</span><span class="sxs-lookup"><span data-stu-id="b09b8-178">In the **Custom Attribute Mapping** section, choose the field you want to map with Azure AD Claim.</span></span> <span data-ttu-id="b09b8-179">In this example, the **emailaddress** claim is mapped with the value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-179">In this example, the **emailaddress** claim is mapped with the value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="b09b8-180">This is the default claim name from Azure AD for email claim.</span><span class="sxs-lookup"><span data-stu-id="b09b8-180">This is the default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="b09b8-181">Use the appropriate **User identifier** to map the user from Azure AD to Docusign user mapping.</span><span class="sxs-lookup"><span data-stu-id="b09b8-181">Use the appropriate **User identifier** to map the user from Azure AD to Docusign user mapping.</span></span> <span data-ttu-id="b09b8-182">Select the proper Field and enter the appropriate value based on your organization settings.</span><span class="sxs-lookup"><span data-stu-id="b09b8-182">Select the proper Field and enter the appropriate value based on your organization settings.</span></span>
    > 
    > 
   
    ![Configuring single sign-on][57]
2. <span data-ttu-id="b09b8-184">In the **Identity Provider Certificate** section, click **Add Certificate**, and then upload the certificate you have downloaded from Azure AD classic portal.</span><span class="sxs-lookup"><span data-stu-id="b09b8-184">In the **Identity Provider Certificate** section, click **Add Certificate**, and then upload the certificate you have downloaded from Azure AD classic portal.</span></span>   
   
    ![Configuring single sign-on][58]
3. <span data-ttu-id="b09b8-186">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-186">Click **Save**.</span></span>
4. <span data-ttu-id="b09b8-187">In the **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-187">In the **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![Configuring single sign-on][59]
5. <span data-ttu-id="b09b8-189">On the Azure classic portal, go back to the **Configure App Settings** page.</span><span class="sxs-lookup"><span data-stu-id="b09b8-189">On the Azure classic portal, go back to the **Configure App Settings** page.</span></span> 
6. <span data-ttu-id="b09b8-190">On **DocuSign admin portal**, in the **View SAML 2.0 Endpoints** section perform, the following steps:</span><span class="sxs-lookup"><span data-stu-id="b09b8-190">On **DocuSign admin portal**, in the **View SAML 2.0 Endpoints** section perform, the following steps:</span></span>
   
    ![Configuring single sign-on][60]
   
    <span data-ttu-id="b09b8-192">a.</span><span class="sxs-lookup"><span data-stu-id="b09b8-192">a.</span></span> <span data-ttu-id="b09b8-193">Copy the **Service Provider Issuer URL**, and then paste it into the **Identifier** textbox on the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="b09b8-193">Copy the **Service Provider Issuer URL**, and then paste it into the **Identifier** textbox on the Azure classic portal.</span></span>
   
    <span data-ttu-id="b09b8-194">b.</span><span class="sxs-lookup"><span data-stu-id="b09b8-194">b.</span></span> <span data-ttu-id="b09b8-195">Copy the **Service Provider Login URL**, and then paste into the **Sign On URL** textbox on the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="b09b8-195">Copy the **Service Provider Login URL**, and then paste into the **Sign On URL** textbox on the Azure classic portal.</span></span>
   
    <span data-ttu-id="b09b8-196">c.</span><span class="sxs-lookup"><span data-stu-id="b09b8-196">c.</span></span>  <span data-ttu-id="b09b8-197">Click **Close**</span><span class="sxs-lookup"><span data-stu-id="b09b8-197">Click **Close**</span></span>  
7. <span data-ttu-id="b09b8-198">On the Azure classic portal, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-198">On the Azure classic portal, click **Next**.</span></span> 
8. <span data-ttu-id="b09b8-199">On the Azure classic portal, select the **Single sign-on configuration confirmation**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-199">On the Azure classic portal, select the **Single sign-on configuration confirmation**, and then click **Next**.</span></span>
   
    ![Applications][14]
9. <span data-ttu-id="b09b8-201">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-201">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![Applications][15]

## <a name="configuring-account-provisioning"></a><span data-ttu-id="b09b8-203">Configuring account provisioning</span><span class="sxs-lookup"><span data-stu-id="b09b8-203">Configuring account provisioning</span></span>
<span data-ttu-id="b09b8-204">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to DocuSign.</span><span class="sxs-lookup"><span data-stu-id="b09b8-204">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to DocuSign.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="b09b8-205">To configure user provisioning, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b09b8-205">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="b09b8-206">In the **Azure classic portal**, on the **DocuSign application integration** page, click **Configure account provisioning** to open the Configure User Provisioning dialog.</span><span class="sxs-lookup"><span data-stu-id="b09b8-206">In the **Azure classic portal**, on the **DocuSign application integration** page, click **Configure account provisioning** to open the Configure User Provisioning dialog.</span></span>
   
    ![Configuring account provisioning][30]
2. <span data-ttu-id="b09b8-208">On the **Settings and admin credentials** page, to enable automatic user provisioning, provide the credentials of a DocuSign account with sufficient rights, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-208">On the **Settings and admin credentials** page, to enable automatic user provisioning, provide the credentials of a DocuSign account with sufficient rights, and then click **Next**.</span></span> 
   
    ![Configuring account provisioning][31]
3. <span data-ttu-id="b09b8-210">On the **Test connection** dialog, click **Start test**, and upon a successful test, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-210">On the **Test connection** dialog, click **Start test**, and upon a successful test, click **Next**.</span></span>
   
    ![Configuring account provisioning][32]
4. <span data-ttu-id="b09b8-212">On the **Confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-212">On the **Confirmation** page, click **Complete**.</span></span>
   
    ![Configuring account provisioning][33]

## <a name="assigning-users"></a><span data-ttu-id="b09b8-214">Assigning users</span><span class="sxs-lookup"><span data-stu-id="b09b8-214">Assigning users</span></span>
<span data-ttu-id="b09b8-215">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="b09b8-215">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-docusign-perform-the-following-steps"></a><span data-ttu-id="b09b8-216">To assign users to DocuSign, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b09b8-216">To assign users to DocuSign, perform the following steps:</span></span>
1. <span data-ttu-id="b09b8-217">In the **Azure classic portal**, create a test account.</span><span class="sxs-lookup"><span data-stu-id="b09b8-217">In the **Azure classic portal**, create a test account.</span></span>
2. <span data-ttu-id="b09b8-218">On the **DocuSign application integration** page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="b09b8-218">On the **DocuSign application integration** page, click **Assign users**.</span></span>
   
    ![Assigning users][40]
3. <span data-ttu-id="b09b8-220">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="b09b8-220">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    ![Assigning users][41]

<span data-ttu-id="b09b8-222">You should now wait for 10 minutes and verify that the account has been synchronized to DocuSign.</span><span class="sxs-lookup"><span data-stu-id="b09b8-222">You should now wait for 10 minutes and verify that the account has been synchronized to DocuSign.</span></span>

<span data-ttu-id="b09b8-223">As a first verification step, you can check the provisioning status, by clicking Dashboard in the D on the DocuSign application integration page on the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="b09b8-223">As a first verification step, you can check the provisioning status, by clicking Dashboard in the D on the DocuSign application integration page on the Azure classic portal.</span></span>

![Assigning users][42]

<span data-ttu-id="b09b8-225">A successfully completed user provisioning cycle is indicated by a related status:</span><span class="sxs-lookup"><span data-stu-id="b09b8-225">A successfully completed user provisioning cycle is indicated by a related status:</span></span>

![Assigning users][43]

<span data-ttu-id="b09b8-227">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b09b8-227">If you want to test your single sign-on settings, open the Access Panel.</span></span>

<span data-ttu-id="b09b8-228">For more details about the Access Panel, see Introduction to the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b09b8-228">For more details about the Access Panel, see Introduction to the Access Panel.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b09b8-229">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="b09b8-229">Additional Resources</span></span>
* [<span data-ttu-id="b09b8-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b09b8-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b09b8-231">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b09b8-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_00.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_01.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_02.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_03.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_04.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_06.png

[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_10.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_11.png

[30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_general_400.png
[31]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_12.png
[32]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_13.png
[33]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_14.png



[40]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_15.png
[41]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_16.png
[42]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_17.png
[43]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_18.png

[51]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
































