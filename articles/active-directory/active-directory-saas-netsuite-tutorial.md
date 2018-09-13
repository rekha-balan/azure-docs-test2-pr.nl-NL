---
title: 'Tutorial: Azure Active Directory integration with Netsuite | Microsoft Docs'
description: Learn how to use Netsuite with Azure Active Directory to enable single sign-on, automated  provisioning, and more!
services: active-directory
documentationcenter: ''
author: asmalser-msft
manager: femila
editor: ''
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2016
ms.author: asmalser
ms.openlocfilehash: eb84385e8a6709aea3b45c18925a2800206a79b8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554551"
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="1c5e1-103">Tutorial: Azure Active Directory integration with Netsuite</span><span class="sxs-lookup"><span data-stu-id="1c5e1-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>
<span data-ttu-id="1c5e1-104">This tutorial will show you how to connect your Netsuite environment to your Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1c5e1-104">This tutorial will show you how to connect your Netsuite environment to your Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="1c5e1-105">You will learn how to configure single sign-on to Netsuite, how to enable automated user provisioning, and how to assign users to have access to Netsuite.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-105">You will learn how to configure single sign-on to Netsuite, how to enable automated user provisioning, and how to assign users to have access to Netsuite.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1c5e1-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1c5e1-106">Prerequisites</span></span>
1. <span data-ttu-id="1c5e1-107">To access Azure Active Directory through the [Azure classic portal](https://manage.windowsazure.com), you must first have a valid Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-107">To access Azure Active Directory through the [Azure classic portal](https://manage.windowsazure.com), you must first have a valid Azure subscription.</span></span>
2. <span data-ttu-id="1c5e1-108">You must have admin access to a [Netsuite](http://www.netsuite.com/portal/home.shtml) subscription.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-108">You must have admin access to a [Netsuite](http://www.netsuite.com/portal/home.shtml) subscription.</span></span> <span data-ttu-id="1c5e1-109">You may use a free trial account for either service.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-109">You may use a free trial account for either service.</span></span>

## <a name="step-1-add-netsuite-to-your-directory"></a><span data-ttu-id="1c5e1-110">Step 1: Add Netsuite to your Directory</span><span class="sxs-lookup"><span data-stu-id="1c5e1-110">Step 1: Add Netsuite to your Directory</span></span>
1. <span data-ttu-id="1c5e1-111">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-111">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Select Active Directory from the left navigation pane.][0]
2. <span data-ttu-id="1c5e1-113">From the **Directory** list, select the directory that you would like to add Netsuite to.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-113">From the **Directory** list, select the directory that you would like to add Netsuite to.</span></span>
3. <span data-ttu-id="1c5e1-114">Click on **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-114">Click on **Applications** in the top menu.</span></span>
   
    ![Click on Applications.][1]
4. <span data-ttu-id="1c5e1-116">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-116">Click **Add** at the bottom of the page.</span></span>
   
    ![Click Add to add a new application.][2]
5. <span data-ttu-id="1c5e1-118">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-118">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Click Add an application from the gallery.][3]
6. <span data-ttu-id="1c5e1-120">In the **search box**, type **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-120">In the **search box**, type **Netsuite**.</span></span> <span data-ttu-id="1c5e1-121">Then select **Netsuite** from the results, and click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-121">Then select **Netsuite** from the results, and click **Complete** to add the application.</span></span>
   
    ![Add Netsuite][4]
7. <span data-ttu-id="1c5e1-123">You should now see the Quick Start page for Netsuite:</span><span class="sxs-lookup"><span data-stu-id="1c5e1-123">You should now see the Quick Start page for Netsuite:</span></span>
   
    ![Netsuite's Quick Start page in Azure AD][5]

## <a name="step-2-enable-single-sign-on"></a><span data-ttu-id="1c5e1-125">Step 2: Enable Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1c5e1-125">Step 2: Enable Single Sign-On</span></span>
1. <span data-ttu-id="1c5e1-126">In Azure AD, on the Quick Start page for Netsuite, click the **Configure single sign-on** button.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-126">In Azure AD, on the Quick Start page for Netsuite, click the **Configure single sign-on** button.</span></span>
   
    ![The configure single sign-on button][6]
2. <span data-ttu-id="1c5e1-128">A dialog will open and you'll see a screen that asks "How would you like users to sign on to Netsuite?"</span><span class="sxs-lookup"><span data-stu-id="1c5e1-128">A dialog will open and you'll see a screen that asks "How would you like users to sign on to Netsuite?"</span></span> <span data-ttu-id="1c5e1-129">Select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-129">Select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Select Azure AD Single Sign-On][7]
   
   > [!NOTE]
   > <span data-ttu-id="1c5e1-131">To learn more about about the different single sign-on options, [click here](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)</span><span class="sxs-lookup"><span data-stu-id="1c5e1-131">To learn more about about the different single sign-on options, [click here](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)</span></span>
   > 
   > 
3. <span data-ttu-id="1c5e1-132">On the **Configure App Settings** page, for the **Reply URL** field, type in your Netsuite tenant URL using one of the following formats:</span><span class="sxs-lookup"><span data-stu-id="1c5e1-132">On the **Configure App Settings** page, for the **Reply URL** field, type in your Netsuite tenant URL using one of the following formats:</span></span>
   
   * `https://<tenant-name>.netsuite.com/saml2/acs`
   * `https://<tenant-name>.na1.netsuite.com/saml2/acs`
   * `https://<tenant-name>.na2.netsuite.com/saml2/acs`
   * `https://<tenant-name>.sandbox.netsuite.com/saml2/acs`
   * `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs`
   * `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`
     
     ![Type in your tenant URL][8]
4. <span data-ttu-id="1c5e1-134">On the **Configure single sign-on at NetSuite** page, click on **Download metadata**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-134">On the **Configure single sign-on at NetSuite** page, click on **Download metadata**, and then save the certificate file locally on your computer.</span></span>
   
    ![Download the metadata.][9]
5. <span data-ttu-id="1c5e1-136">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-136">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>
6. <span data-ttu-id="1c5e1-137">In the toolbar at the top of the page, click **Setup**, then click **Setup Manager**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-137">In the toolbar at the top of the page, click **Setup**, then click **Setup Manager**.</span></span>
   
    ![Go to Setup Manager][10]
7. <span data-ttu-id="1c5e1-139">From the **Setup Tasks** list, select **Integration**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-139">From the **Setup Tasks** list, select **Integration**.</span></span>
   
    ![Go to Integration][11]
8. <span data-ttu-id="1c5e1-141">In the **Manage Authentication** section, click **SAML Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-141">In the **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>
   
    ![Go to SAML Single Sign-on][12]
9. <span data-ttu-id="1c5e1-143">On the **SAML Setup** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1c5e1-143">On the **SAML Setup** page, perform the following steps:</span></span>
   
   * <span data-ttu-id="1c5e1-144">In Azure Active Directory, copy the **Remote Login URL** value and paste it into the **Identity Provider Login Page** field in Netsuite.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-144">In Azure Active Directory, copy the **Remote Login URL** value and paste it into the **Identity Provider Login Page** field in Netsuite.</span></span>
     
       ![The SAML Setup page.][13]
   * <span data-ttu-id="1c5e1-146">In Netsuite, select **Primary Authentication Method**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-146">In Netsuite, select **Primary Authentication Method**.</span></span>
   * <span data-ttu-id="1c5e1-147">For the field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-147">For the field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="1c5e1-148">Then click **Browse** to upload the metadata file that you downloaded in step #4.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-148">Then click **Browse** to upload the metadata file that you downloaded in step #4.</span></span>
     
       ![Upload the metadata][16]
   * <span data-ttu-id="1c5e1-150">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-150">Click **Submit**.</span></span>
10. <span data-ttu-id="1c5e1-151">In Azure AD, select the single sign-on configuration confirmation checkbox to enable the certificate that you uploaded to Netsuite.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-151">In Azure AD, select the single sign-on configuration confirmation checkbox to enable the certificate that you uploaded to Netsuite.</span></span> <span data-ttu-id="1c5e1-152">Then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-152">Then click **Next**.</span></span>
    
     ![Check the confirmation checkbox][14]
11. <span data-ttu-id="1c5e1-154">On the final page of the dialog, type in an email address if you would like to receive email notifications for errors and warnings related to the maintenance of this single sign-on configuration.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-154">On the final page of the dialog, type in an email address if you would like to receive email notifications for errors and warnings related to the maintenance of this single sign-on configuration.</span></span> 
    
    ![Type in your email address.][15]
12. <span data-ttu-id="1c5e1-156">Click **Complete** to close the dialog.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-156">Click **Complete** to close the dialog.</span></span> <span data-ttu-id="1c5e1-157">Next, click on **Attributes** at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-157">Next, click on **Attributes** at the top of the page.</span></span>
    
    ![Click on Attributes.][17]
13. <span data-ttu-id="1c5e1-159">Click on **Add User Attribute**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-159">Click on **Add User Attribute**.</span></span>
    
    ![Click on Add User Attribute.][18]
14. <span data-ttu-id="1c5e1-161">For the **Attribute Name** field, type in `account`.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-161">For the **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="1c5e1-162">For the **Attribute Value** field, type in your Netsuite account ID.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-162">For the **Attribute Value** field, type in your Netsuite account ID.</span></span> <span data-ttu-id="1c5e1-163">Instructions on how to find your account ID are included below:</span><span class="sxs-lookup"><span data-stu-id="1c5e1-163">Instructions on how to find your account ID are included below:</span></span>
    
    ![Add your Netsuite Account ID.][19]
    
    * <span data-ttu-id="1c5e1-165">In Netsuite, click on **Setup** from the top navigation menu.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-165">In Netsuite, click on **Setup** from the top navigation menu.</span></span>
    * <span data-ttu-id="1c5e1-166">Then click under the **Setup Tasks** section of the left navigation menu, select the **Integration** section, and click on **Web Services Preferences**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-166">Then click under the **Setup Tasks** section of the left navigation menu, select the **Integration** section, and click on **Web Services Preferences**.</span></span>
    * <span data-ttu-id="1c5e1-167">Copy your Netsuite Account ID and paste it into the **Attribute Value** field in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-167">Copy your Netsuite Account ID and paste it into the **Attribute Value** field in Azure AD.</span></span>
      
        ![Get your account ID][20]
15. <span data-ttu-id="1c5e1-169">In Azure AD, click **Complete** to finish adding the SAML attribute.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-169">In Azure AD, click **Complete** to finish adding the SAML attribute.</span></span> <span data-ttu-id="1c5e1-170">Then click **Apply Changes** on the bottom menu.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-170">Then click **Apply Changes** on the bottom menu.</span></span>
    
    ![Save your changes.][21]
16. <span data-ttu-id="1c5e1-172">Before users can perform single sign-on into Netsuite, they must first be assigned the appropriate permissions in Netsuite.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-172">Before users can perform single sign-on into Netsuite, they must first be assigned the appropriate permissions in Netsuite.</span></span> <span data-ttu-id="1c5e1-173">Follow the instructions below to assign these permissions.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-173">Follow the instructions below to assign these permissions.</span></span>
    
    * <span data-ttu-id="1c5e1-174">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-174">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
        ![Go to Setup Manager][10]
    * <span data-ttu-id="1c5e1-176">On the left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-176">On the left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
        ![Go to Manage Roles][22]
    * <span data-ttu-id="1c5e1-178">Click **New Role**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-178">Click **New Role**.</span></span>
    * <span data-ttu-id="1c5e1-179">Type in a **Name** for you new role, and select the **Single Sign-On Only** checkbox.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-179">Type in a **Name** for you new role, and select the **Single Sign-On Only** checkbox.</span></span>
      
        ![Name the new role.][23]
    * <span data-ttu-id="1c5e1-181">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-181">Click **Save**.</span></span>
    * <span data-ttu-id="1c5e1-182">In the menu on the top, click **Permissions**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-182">In the menu on the top, click **Permissions**.</span></span> <span data-ttu-id="1c5e1-183">Then click **Setup**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-183">Then click **Setup**.</span></span>
      
        ![Go to Permissions][24]
    * <span data-ttu-id="1c5e1-185">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-185">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>
    * <span data-ttu-id="1c5e1-186">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-186">Click **Save**.</span></span>
    * <span data-ttu-id="1c5e1-187">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-187">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
        ![Go to Setup Manager][10]
    * <span data-ttu-id="1c5e1-189">On the left navigation menu, select **Users/Roles**, then click **Manage Users**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-189">On the left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
        ![Go to Manage Users][25]
    * <span data-ttu-id="1c5e1-191">Select a test user.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-191">Select a test user.</span></span> <span data-ttu-id="1c5e1-192">Then click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-192">Then click **Edit**.</span></span>
      
        ![Go to Manage Users][26]
    * <span data-ttu-id="1c5e1-194">On the Roles dialog, select the role that you have created and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-194">On the Roles dialog, select the role that you have created and click **Add**.</span></span>
      
        ![Go to Manage Users][27]
    * <span data-ttu-id="1c5e1-196">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-196">Click **Save**.</span></span>
17. <span data-ttu-id="1c5e1-197">To test your configuration, see the section below titled [Assign Users to Netsuite](#step-4-assign-users-to-netsuite).</span><span class="sxs-lookup"><span data-stu-id="1c5e1-197">To test your configuration, see the section below titled [Assign Users to Netsuite](#step-4-assign-users-to-netsuite).</span></span>

## <a name="step-3-enable-automated-user-provisioning"></a><span data-ttu-id="1c5e1-198">Step 3: Enable Automated User Provisioning</span><span class="sxs-lookup"><span data-stu-id="1c5e1-198">Step 3: Enable Automated User Provisioning</span></span>
> [!NOTE]
> <span data-ttu-id="1c5e1-199">By default, your provisioned users will be added to the root subsidiary of your Netsuite environment.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-199">By default, your provisioned users will be added to the root subsidiary of your Netsuite environment.</span></span>
> 
> 

1. <span data-ttu-id="1c5e1-200">In Azure Active Directory, on the Quick Start page for Netsuite, click on **Configure user provisioning**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-200">In Azure Active Directory, on the Quick Start page for Netsuite, click on **Configure user provisioning**.</span></span>
   
    ![Configure user provisioning][28]
2. <span data-ttu-id="1c5e1-202">In the dialog that opens, type in your admin credentials for Netsuite, then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-202">In the dialog that opens, type in your admin credentials for Netsuite, then click **Next**.</span></span>
   
    ![Type in your Netsuite admin credentials.][29]
3. <span data-ttu-id="1c5e1-204">On the confirmation page, type in your email address to receive notifications of provisioning failures.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-204">On the confirmation page, type in your email address to receive notifications of provisioning failures.</span></span>
   
    ![Confirm.][30]
4. <span data-ttu-id="1c5e1-206">Click **Complete** to close the dialog.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-206">Click **Complete** to close the dialog.</span></span>

## <a name="step-4-assign-users-to-netsuite"></a><span data-ttu-id="1c5e1-207">Step 4: Assign Users to Netsuite</span><span class="sxs-lookup"><span data-stu-id="1c5e1-207">Step 4: Assign Users to Netsuite</span></span>
1. <span data-ttu-id="1c5e1-208">To test your configuration, start creating a new test account in the directory.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-208">To test your configuration, start creating a new test account in the directory.</span></span>
2. <span data-ttu-id="1c5e1-209">On the Netsuite Quick Start page, click on the **Assign Users** button.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-209">On the Netsuite Quick Start page, click on the **Assign Users** button.</span></span>
   
    ![Click on Assign Users][31]
3. <span data-ttu-id="1c5e1-211">Select your test user, and click the **Assign** button at the bottom of the screen:</span><span class="sxs-lookup"><span data-stu-id="1c5e1-211">Select your test user, and click the **Assign** button at the bottom of the screen:</span></span>
   
   * <span data-ttu-id="1c5e1-212">If you haven't enable automated user provisioning, then you'll see the following prompt to confirm:</span><span class="sxs-lookup"><span data-stu-id="1c5e1-212">If you haven't enable automated user provisioning, then you'll see the following prompt to confirm:</span></span>
     
        ![Confirm the assignment.][32]
   * <span data-ttu-id="1c5e1-214">If you have enabled automated user provisioning, then you'll see a prompt to define what type of role the user should have in Netsuite.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-214">If you have enabled automated user provisioning, then you'll see a prompt to define what type of role the user should have in Netsuite.</span></span> <span data-ttu-id="1c5e1-215">Newly provisioned users should appear in your Netsuite environment after a few minutes.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-215">Newly provisioned users should appear in your Netsuite environment after a few minutes.</span></span>
4. <span data-ttu-id="1c5e1-216">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into the test account, and click on **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="1c5e1-216">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into the test account, and click on **Netsuite**.</span></span>

## <a name="related-articles"></a><span data-ttu-id="1c5e1-217">Related Articles</span><span class="sxs-lookup"><span data-stu-id="1c5e1-217">Related Articles</span></span>
* [<span data-ttu-id="1c5e1-218">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c5e1-218">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="1c5e1-219">List of Tutorials on How to Integrate SaaS Apps</span><span class="sxs-lookup"><span data-stu-id="1c5e1-219">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/azure-active-directory.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/applications-tab.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/add-app.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/add-app-gallery.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/add-netsuite.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/quick-start-netsuite.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/config-sso.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/sso-netsuite.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/sso-config-netsuite.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/config-sso-netsuite.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/ns-setup.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/ns-integration.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/ns-saml.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/ns-sso-confirm.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/sso-email.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/ns-attributes.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/ns-add-attribute.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/ns-add-account.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/ns-account-id.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/ns-save-saml.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/ns-manage-roles.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/ns-new-role.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/ns-sso.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/ns-manage-users.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/ns-edit-user.png
[27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/ns-add-role.png
[28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/netsuite-provisioning.png
[29]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/ns-creds.png
[30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/ns-confirm.png
[31]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/assign-users.png
[32]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-netsuite-tutorial/assign-confirm.png

































