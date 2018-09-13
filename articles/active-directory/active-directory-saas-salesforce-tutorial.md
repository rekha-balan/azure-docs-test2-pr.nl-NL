---
title: 'Tutorial: Azure Active Directory integration with Salesforce | Microsoft Docs'
description: Learn how to use Salesforce with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
documentationcenter: ''
author: asmalser-msft
manager: femila
editor: ''
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2016
ms.author: asmalser
ms.openlocfilehash: a2e85596df127ce424a80932b88d6443254e4206
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549387"
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="0a09b-103">Tutorial: Azure Active Directory integration with Salesforce</span><span class="sxs-lookup"><span data-stu-id="0a09b-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>
<span data-ttu-id="0a09b-104">This tutorial will show you how to connect your Salesforce environment to your Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0a09b-104">This tutorial will show you how to connect your Salesforce environment to your Azure Active Directory.</span></span> <span data-ttu-id="0a09b-105">You will learn how to configure single sign-on to Salesforce, how to enable automated user provisioning, and how to assign users to have access to Salesforce.</span><span class="sxs-lookup"><span data-stu-id="0a09b-105">You will learn how to configure single sign-on to Salesforce, how to enable automated user provisioning, and how to assign users to have access to Salesforce.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a09b-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0a09b-106">Prerequisites</span></span>
1. <span data-ttu-id="0a09b-107">To access Azure Active Directory through the [Azure classic portal](https://manage.windowsazure.com), you must first have a valid Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0a09b-107">To access Azure Active Directory through the [Azure classic portal](https://manage.windowsazure.com), you must first have a valid Azure subscription.</span></span>
2. <span data-ttu-id="0a09b-108">You must have a valid tenant in [Salesforce.com](https://www.salesforce.com/).</span><span class="sxs-lookup"><span data-stu-id="0a09b-108">You must have a valid tenant in [Salesforce.com](https://www.salesforce.com/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a09b-109">If you are using a Salesforce.com **trial** account, then you will be unable to configure automated user provisioning.</span><span class="sxs-lookup"><span data-stu-id="0a09b-109">If you are using a Salesforce.com **trial** account, then you will be unable to configure automated user provisioning.</span></span> <span data-ttu-id="0a09b-110">Trial accounts do not have the necessary API access enabled until they are purchased.</span><span class="sxs-lookup"><span data-stu-id="0a09b-110">Trial accounts do not have the necessary API access enabled until they are purchased.</span></span>
> 
> <span data-ttu-id="0a09b-111">You can get around this limitation by using a [free developer account](https://developer.salesforce.com/signup) to complete this tutorial.</span><span class="sxs-lookup"><span data-stu-id="0a09b-111">You can get around this limitation by using a [free developer account](https://developer.salesforce.com/signup) to complete this tutorial.</span></span>
> 
> 

<span data-ttu-id="0a09b-112">If you are using a Salesforce Sandbox environment, please see the [Salesforce Sandbox integration tutorial](https://go.microsoft.com/fwLink/?LinkID=521879).</span><span class="sxs-lookup"><span data-stu-id="0a09b-112">If you are using a Salesforce Sandbox environment, please see the [Salesforce Sandbox integration tutorial](https://go.microsoft.com/fwLink/?LinkID=521879).</span></span>

## <a name="video-tutorials"></a><span data-ttu-id="0a09b-113">Video tutorials</span><span class="sxs-lookup"><span data-stu-id="0a09b-113">Video tutorials</span></span>
<span data-ttu-id="0a09b-114">You may follow this tutorial using the videos below.</span><span class="sxs-lookup"><span data-stu-id="0a09b-114">You may follow this tutorial using the videos below.</span></span>

<span data-ttu-id="0a09b-115">**Video Tutorial Part One: How to Enable Single Sign-On**</span><span class="sxs-lookup"><span data-stu-id="0a09b-115">**Video Tutorial Part One: How to Enable Single Sign-On**</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Integrating-Salesforce-with-Azure-AD-How-to-enable-Single-Sign-On-12/player]
> 
> 

<span data-ttu-id="0a09b-116">**Video Tutorial Part Two: How to Automate User Provisioning**</span><span class="sxs-lookup"><span data-stu-id="0a09b-116">**Video Tutorial Part Two: How to Automate User Provisioning**</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Integrating-Salesforce-with-Azure-AD-How-to-automate-User-Provisioning-22/player]
> 
> 

## <a name="step-1-add-salesforce-to-your-directory"></a><span data-ttu-id="0a09b-117">Step 1: Add Salesforce to your directory</span><span class="sxs-lookup"><span data-stu-id="0a09b-117">Step 1: Add Salesforce to your directory</span></span>
1. <span data-ttu-id="0a09b-118">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0a09b-118">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Select Active Directory from the left navigation pane.][0]
2. <span data-ttu-id="0a09b-120">From the **Directory** list, select the directory that you would like to add Salesforce to.</span><span class="sxs-lookup"><span data-stu-id="0a09b-120">From the **Directory** list, select the directory that you would like to add Salesforce to.</span></span>
3. <span data-ttu-id="0a09b-121">Click on **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="0a09b-121">Click on **Applications** in the top menu.</span></span>
   
    ![Click on Applications.][1]
4. <span data-ttu-id="0a09b-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="0a09b-123">Click **Add** at the bottom of the page.</span></span>
   
    ![Click Add to add a new application.][2]
5. <span data-ttu-id="0a09b-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="0a09b-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Click Add an application from the gallery.][3]
6. <span data-ttu-id="0a09b-127">In the **search box**, type **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="0a09b-127">In the **search box**, type **Salesforce**.</span></span> <span data-ttu-id="0a09b-128">Then select **Salesforce** from the results, and click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="0a09b-128">Then select **Salesforce** from the results, and click **Complete** to add the application.</span></span>
   
    ![Add Salesforce.][4]
7. <span data-ttu-id="0a09b-130">You should now see the Quick Start page for Salesforce:</span><span class="sxs-lookup"><span data-stu-id="0a09b-130">You should now see the Quick Start page for Salesforce:</span></span>
   
    ![Salesforce's Quick Start page in Azure AD][5]

## <a name="step-2-enable-single-sign-on"></a><span data-ttu-id="0a09b-132">Step 2: Enable single sign-on</span><span class="sxs-lookup"><span data-stu-id="0a09b-132">Step 2: Enable single sign-on</span></span>
1. <span data-ttu-id="0a09b-133">Before you can configure single sign-on, you must set up and deploy a custom domain for your Salesforce environment.</span><span class="sxs-lookup"><span data-stu-id="0a09b-133">Before you can configure single sign-on, you must set up and deploy a custom domain for your Salesforce environment.</span></span> <span data-ttu-id="0a09b-134">For instructions on how to do that, see [Set Up a Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_setup.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="0a09b-134">For instructions on how to do that, see [Set Up a Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_setup.htm&language=en_US).</span></span>
2. <span data-ttu-id="0a09b-135">On Salesforce's Quick Start page in Azure AD, click the **Configure single sign-on** button.</span><span class="sxs-lookup"><span data-stu-id="0a09b-135">On Salesforce's Quick Start page in Azure AD, click the **Configure single sign-on** button.</span></span>
   
    ![The configure single sign-on button][6]
3. <span data-ttu-id="0a09b-137">A dialog will open and you'll see a screen that asks "How would you like users to sign on to Salesforce?"</span><span class="sxs-lookup"><span data-stu-id="0a09b-137">A dialog will open and you'll see a screen that asks "How would you like users to sign on to Salesforce?"</span></span> <span data-ttu-id="0a09b-138">Select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0a09b-138">Select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Select Azure AD Single Sign-On][7]
   
   > [!NOTE]
   > <span data-ttu-id="0a09b-140">To learn more about about the different single sign-on options, [click here](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)</span><span class="sxs-lookup"><span data-stu-id="0a09b-140">To learn more about about the different single sign-on options, [click here](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)</span></span>
   > 
   > 
4. <span data-ttu-id="0a09b-141">On the **Configure App Settings** page, fill out the **Sign On URL** by typing in your Salesforce domain URL using the following format:</span><span class="sxs-lookup"><span data-stu-id="0a09b-141">On the **Configure App Settings** page, fill out the **Sign On URL** by typing in your Salesforce domain URL using the following format:</span></span>
   
   * <span data-ttu-id="0a09b-142">Enterprise account: `https://<domain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="0a09b-142">Enterprise account: `https://<domain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="0a09b-143">Developer account: `https://<domain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="0a09b-143">Developer account: `https://<domain>-dev-ed.my.salesforce.com`</span></span> 
     
     ![Type in your Sign On URL][8]
5. <span data-ttu-id="0a09b-145">On the **Configure single sign-on at Salesforce** page, click on **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="0a09b-145">On the **Configure single sign-on at Salesforce** page, click on **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![Download certificate][9]
6. <span data-ttu-id="0a09b-147">Open a new tab in your browser and log in to your Salesforce administrator account.</span><span class="sxs-lookup"><span data-stu-id="0a09b-147">Open a new tab in your browser and log in to your Salesforce administrator account.</span></span>
7. <span data-ttu-id="0a09b-148">Under the **Administrator** navigation pane, click **Security Controls** to expand the related section.</span><span class="sxs-lookup"><span data-stu-id="0a09b-148">Under the **Administrator** navigation pane, click **Security Controls** to expand the related section.</span></span> <span data-ttu-id="0a09b-149">Then click on **Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="0a09b-149">Then click on **Single Sign-On Settings**.</span></span>
   
    ![Click on Single Sign-On Settings under Security Controls][10]
8. <span data-ttu-id="0a09b-151">On the **Single Sign-On Settings** page, click the **Edit** button.</span><span class="sxs-lookup"><span data-stu-id="0a09b-151">On the **Single Sign-On Settings** page, click the **Edit** button.</span></span>
   
    ![Click the Edit button][11]
   
   > [!NOTE]
   > <span data-ttu-id="0a09b-153">If you are unable to enable Single Sign-On settings for your Salesforce account, you may need to contact Salesforce's support in order to have the feature enabled for you.</span><span class="sxs-lookup"><span data-stu-id="0a09b-153">If you are unable to enable Single Sign-On settings for your Salesforce account, you may need to contact Salesforce's support in order to have the feature enabled for you.</span></span>
   > 
   > 
9. <span data-ttu-id="0a09b-154">Select **SAML Enabled**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="0a09b-154">Select **SAML Enabled**, and then click **Save**.</span></span>
   
    ![Select SAML Enabled][12]
10. <span data-ttu-id="0a09b-156">To configure your SAML single sign-on settings, click **New**.</span><span class="sxs-lookup"><span data-stu-id="0a09b-156">To configure your SAML single sign-on settings, click **New**.</span></span>
    
    ![Select SAML Enabled][13]
11. <span data-ttu-id="0a09b-158">On the **SAML Single Sign-On Setting Edit** page, make the following configurations:</span><span class="sxs-lookup"><span data-stu-id="0a09b-158">On the **SAML Single Sign-On Setting Edit** page, make the following configurations:</span></span>
    
    ![Screenshot of the configurations that you should make][14]
    
    * <span data-ttu-id="0a09b-160">For the **Name** field, type in a friendly name for this configuration.</span><span class="sxs-lookup"><span data-stu-id="0a09b-160">For the **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="0a09b-161">Providing a value for **Name** automatically populate the **API Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="0a09b-161">Providing a value for **Name** automatically populate the **API Name** textbox.</span></span>
    * <span data-ttu-id="0a09b-162">In Azure AD, copy the **Issuer URL** value, and then paste it into the **Issuer** field in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="0a09b-162">In Azure AD, copy the **Issuer URL** value, and then paste it into the **Issuer** field in Salesforce.</span></span>
    * <span data-ttu-id="0a09b-163">In the **Entity Id textbox**, type your Salesforce domain name using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="0a09b-163">In the **Entity Id textbox**, type your Salesforce domain name using the following pattern:</span></span>
      
      * <span data-ttu-id="0a09b-164">Enterprise account: `https://<domain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="0a09b-164">Enterprise account: `https://<domain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="0a09b-165">Developer account: `https://<domain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="0a09b-165">Developer account: `https://<domain>-dev-ed.my.salesforce.com`</span></span>
    * <span data-ttu-id="0a09b-166">Click **Browse** or **Choose File** to open the **Choose File to Upload** dialog, select your Salesforce certificate, and then click **Open** to upload the certificate.</span><span class="sxs-lookup"><span data-stu-id="0a09b-166">Click **Browse** or **Choose File** to open the **Choose File to Upload** dialog, select your Salesforce certificate, and then click **Open** to upload the certificate.</span></span>
    * <span data-ttu-id="0a09b-167">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span><span class="sxs-lookup"><span data-stu-id="0a09b-167">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>
    * <span data-ttu-id="0a09b-168">For **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**</span><span class="sxs-lookup"><span data-stu-id="0a09b-168">For **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**</span></span>
    * <span data-ttu-id="0a09b-169">In Azure AD, copy the **Remote Login URL** value, and then paste it into the **Identity Provider Login URL** field in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="0a09b-169">In Azure AD, copy the **Remote Login URL** value, and then paste it into the **Identity Provider Login URL** field in Salesforce.</span></span>
    * <span data-ttu-id="0a09b-170">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span><span class="sxs-lookup"><span data-stu-id="0a09b-170">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    * <span data-ttu-id="0a09b-171">Finally, click **Save** to apply your SAML single sign-on settings.</span><span class="sxs-lookup"><span data-stu-id="0a09b-171">Finally, click **Save** to apply your SAML single sign-on settings.</span></span>
12. <span data-ttu-id="0a09b-172">On the left navigation pane in Salesforce, click **Domain Management** to expand the related section, and then click **My Domain**.</span><span class="sxs-lookup"><span data-stu-id="0a09b-172">On the left navigation pane in Salesforce, click **Domain Management** to expand the related section, and then click **My Domain**.</span></span>
    
    ![Click on My Domain][15]
13. <span data-ttu-id="0a09b-174">Scroll down to the **Authentication Configuration** section, and click the **Edit** button.</span><span class="sxs-lookup"><span data-stu-id="0a09b-174">Scroll down to the **Authentication Configuration** section, and click the **Edit** button.</span></span>
    
    ![Click the Edit button][16]
14. <span data-ttu-id="0a09b-176">In the **Authentication Service** section, select the friendly name of your SAML SSO configuration, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="0a09b-176">In the **Authentication Service** section, select the friendly name of your SAML SSO configuration, and then click **Save**.</span></span>
    
    ![Select your SSO configuration][17]
    
    > [!NOTE]
    > <span data-ttu-id="0a09b-178">If more than one authentication service is selected, then when users attempt to initiate single sign-on to your Salesforce environment, they will be prompted to select which authentication service they would like to sign in with.</span><span class="sxs-lookup"><span data-stu-id="0a09b-178">If more than one authentication service is selected, then when users attempt to initiate single sign-on to your Salesforce environment, they will be prompted to select which authentication service they would like to sign in with.</span></span> <span data-ttu-id="0a09b-179">If you don’t want this to happen, then you should **leave all other authentication services unchecked**.</span><span class="sxs-lookup"><span data-stu-id="0a09b-179">If you don’t want this to happen, then you should **leave all other authentication services unchecked**.</span></span>
    > 
    > 
15. <span data-ttu-id="0a09b-180">In Azure AD, select the single sign-on configuration confirmation checkbox to enable the certificate that you uploaded to Salesforce.</span><span class="sxs-lookup"><span data-stu-id="0a09b-180">In Azure AD, select the single sign-on configuration confirmation checkbox to enable the certificate that you uploaded to Salesforce.</span></span> <span data-ttu-id="0a09b-181">Then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0a09b-181">Then click **Next**.</span></span>
    
    ![Check the confirmation checkbox][18]
16. <span data-ttu-id="0a09b-183">On the final page of the dialog, type in an email address if you would like to receive email notifications for errors and warnings related to the maintenance of this single sign-on configuration.</span><span class="sxs-lookup"><span data-stu-id="0a09b-183">On the final page of the dialog, type in an email address if you would like to receive email notifications for errors and warnings related to the maintenance of this single sign-on configuration.</span></span> 
    
    ![Type in your email address.][19]
17. <span data-ttu-id="0a09b-185">Click **Complete** to close the dialog.</span><span class="sxs-lookup"><span data-stu-id="0a09b-185">Click **Complete** to close the dialog.</span></span> <span data-ttu-id="0a09b-186">To test your configuration, see the section below titled [Assign Users to Salesforce](#step-4-assign-users-to-salesforce).</span><span class="sxs-lookup"><span data-stu-id="0a09b-186">To test your configuration, see the section below titled [Assign Users to Salesforce](#step-4-assign-users-to-salesforce).</span></span>

## <a name="step-3-enable-automated-user-provisioning"></a><span data-ttu-id="0a09b-187">Step 3: Enable automated user provisioning</span><span class="sxs-lookup"><span data-stu-id="0a09b-187">Step 3: Enable automated user provisioning</span></span>
1. <span data-ttu-id="0a09b-188">In the Azure AD Quick Start page for Salesforce, click on the **Configure user provisioning** button.</span><span class="sxs-lookup"><span data-stu-id="0a09b-188">In the Azure AD Quick Start page for Salesforce, click on the **Configure user provisioning** button.</span></span>
   
    ![Click the Configure User Provisioning button][20]
2. <span data-ttu-id="0a09b-190">In the **Configure user provisioning** dialog, type in your Salesforce admin username and password.</span><span class="sxs-lookup"><span data-stu-id="0a09b-190">In the **Configure user provisioning** dialog, type in your Salesforce admin username and password.</span></span>
   
    ![Type in your admin username or password][21]
   
   > [!NOTE]
   > <span data-ttu-id="0a09b-192">If you are configuring a production environment, the best practice is to create a new admin account in Salesforce specifically for this step.</span><span class="sxs-lookup"><span data-stu-id="0a09b-192">If you are configuring a production environment, the best practice is to create a new admin account in Salesforce specifically for this step.</span></span> <span data-ttu-id="0a09b-193">This account must have the **System Administrator** profile assigned to it in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="0a09b-193">This account must have the **System Administrator** profile assigned to it in Salesforce.</span></span>
   > 
   > 
3. <span data-ttu-id="0a09b-194">To get your Salesforce security token, open a new tab and sign into the same Salesforce admin account.</span><span class="sxs-lookup"><span data-stu-id="0a09b-194">To get your Salesforce security token, open a new tab and sign into the same Salesforce admin account.</span></span> <span data-ttu-id="0a09b-195">On the top right corner of the page, click on your name, and then click on **My Settings**.</span><span class="sxs-lookup"><span data-stu-id="0a09b-195">On the top right corner of the page, click on your name, and then click on **My Settings**.</span></span>
   
    ![Click on your name, then click on My Settings][22]
4. <span data-ttu-id="0a09b-197">On the left navigation pane, click on **Personal** to expand the related section, and then click on **Reset My Security Token**.</span><span class="sxs-lookup"><span data-stu-id="0a09b-197">On the left navigation pane, click on **Personal** to expand the related section, and then click on **Reset My Security Token**.</span></span>
   
    ![Click on your name, then click on My Settings][23]
5. <span data-ttu-id="0a09b-199">On the **Reset My Security Token** page, click on the **Reset Security Token** button.</span><span class="sxs-lookup"><span data-stu-id="0a09b-199">On the **Reset My Security Token** page, click on the **Reset Security Token** button.</span></span>
   
    ![Read the warnings.][24]
6. <span data-ttu-id="0a09b-201">Check the email inbox associated with this admin account.</span><span class="sxs-lookup"><span data-stu-id="0a09b-201">Check the email inbox associated with this admin account.</span></span> <span data-ttu-id="0a09b-202">Look for an email from Salesforce.com that contains the new security token.</span><span class="sxs-lookup"><span data-stu-id="0a09b-202">Look for an email from Salesforce.com that contains the new security token.</span></span>
7. <span data-ttu-id="0a09b-203">Copy the token, go to your Azure AD window, and paste it into the **User Security Token** field.</span><span class="sxs-lookup"><span data-stu-id="0a09b-203">Copy the token, go to your Azure AD window, and paste it into the **User Security Token** field.</span></span> <span data-ttu-id="0a09b-204">Then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0a09b-204">Then click **Next**.</span></span>
   
    ![Paste in the security token][25]
8. <span data-ttu-id="0a09b-206">On the confirmation page, you can choose to receive email notifications for when provisioning failures occur.</span><span class="sxs-lookup"><span data-stu-id="0a09b-206">On the confirmation page, you can choose to receive email notifications for when provisioning failures occur.</span></span> <span data-ttu-id="0a09b-207">Click **Complete** to close the dialog.</span><span class="sxs-lookup"><span data-stu-id="0a09b-207">Click **Complete** to close the dialog.</span></span>
   
    ![Type in your email address to receive notifications][26]

## <a name="step-4-assign-users-to-salesforce"></a><span data-ttu-id="0a09b-209">Step 4: Assign users to Salesforce</span><span class="sxs-lookup"><span data-stu-id="0a09b-209">Step 4: Assign users to Salesforce</span></span>
1. <span data-ttu-id="0a09b-210">To test your configuration, start by creating a new test account in the directory.</span><span class="sxs-lookup"><span data-stu-id="0a09b-210">To test your configuration, start by creating a new test account in the directory.</span></span>
2. <span data-ttu-id="0a09b-211">On the Salesforce Quick Start page, click on the **Assign Users** button.</span><span class="sxs-lookup"><span data-stu-id="0a09b-211">On the Salesforce Quick Start page, click on the **Assign Users** button.</span></span>
   
    ![Click on Assign Users][27]
3. <span data-ttu-id="0a09b-213">Select your test user, and click the **Assign** button at the bottom of the screen:</span><span class="sxs-lookup"><span data-stu-id="0a09b-213">Select your test user, and click the **Assign** button at the bottom of the screen:</span></span>
   
   * <span data-ttu-id="0a09b-214">If you haven't enable automated user provisioning, then you'll see the following prompt to confirm:</span><span class="sxs-lookup"><span data-stu-id="0a09b-214">If you haven't enable automated user provisioning, then you'll see the following prompt to confirm:</span></span>
     
        ![Confirm the assignment.][28]
   * <span data-ttu-id="0a09b-216">If you have enabled automated user provisioning, then you'll see a prompt to define what type of Salesforce profile the user should have.</span><span class="sxs-lookup"><span data-stu-id="0a09b-216">If you have enabled automated user provisioning, then you'll see a prompt to define what type of Salesforce profile the user should have.</span></span> <span data-ttu-id="0a09b-217">Newly provisioned users should appear in your Salesforce environment after a few minutes.</span><span class="sxs-lookup"><span data-stu-id="0a09b-217">Newly provisioned users should appear in your Salesforce environment after a few minutes.</span></span>
     
        ![Confirm the assignment.][29]
     
     > [!IMPORTANT]
     > <span data-ttu-id="0a09b-219">If you are provisioning to a Salesforce **developer** environment, you will have a very limited number of licenses available for each profile.</span><span class="sxs-lookup"><span data-stu-id="0a09b-219">If you are provisioning to a Salesforce **developer** environment, you will have a very limited number of licenses available for each profile.</span></span> <span data-ttu-id="0a09b-220">Therefore, it's best to provision users to the **Chatter Free User** profile, which has 4,999 licenses available.</span><span class="sxs-lookup"><span data-stu-id="0a09b-220">Therefore, it's best to provision users to the **Chatter Free User** profile, which has 4,999 licenses available.</span></span>
     > 
     > 
4. <span data-ttu-id="0a09b-221">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into the test account, and click on **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="0a09b-221">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into the test account, and click on **Salesforce**.</span></span>

## <a name="related-articles"></a><span data-ttu-id="0a09b-222">Related Articles</span><span class="sxs-lookup"><span data-stu-id="0a09b-222">Related Articles</span></span>
* [<span data-ttu-id="0a09b-223">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a09b-223">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="0a09b-224">List of Tutorials on How to Integrate SaaS Apps</span><span class="sxs-lookup"><span data-stu-id="0a09b-224">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/azure-active-directory.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/applications-tab.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/add-app.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/add-app-gallery.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/add-salesforce.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/salesforce-added.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/config-sso.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/select-azure-ad-sso.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/config-app-settings.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/download-certificate.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/sf-saml-config.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/sf-my-domain.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/sf-auth-config.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/sso-confirm.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/sso-notification.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/config-prov.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/config-prov-dialog.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/sf-my-settings.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/sf-personal-reset.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/sf-reset-token.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/got-the-token.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/prov-confirm.png
[27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/assign-users.png
[28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/assign-confirm.png
[29]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-salesforce-tutorial/assign-sf-profile.png






























