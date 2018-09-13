---
title: 'Tutorial: Azure Active Directory integration with Google Apps | Microsoft Docs'
description: Learn how to use Google Apps with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
documentationcenter: ''
author: asmalser-msft
manager: femila
editor: ''
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2016
ms.author: asmalser
ms.openlocfilehash: 384b4c7e47afcf2664fabc1c98b888a349dd5aaf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554984"
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a><span data-ttu-id="5cca6-103">Tutorial: Azure Active Directory integration with Google Apps</span><span class="sxs-lookup"><span data-stu-id="5cca6-103">Tutorial: Azure Active Directory integration with Google Apps</span></span>
<span data-ttu-id="5cca6-104">This tutorial will show you how to connect your Google Apps environment to your Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5cca6-104">This tutorial will show you how to connect your Google Apps environment to your Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="5cca6-105">You will learn how to configure single sign-on to Google Apps, how to enable automated user provisioning, and how to assign users to have access to Google Apps.</span><span class="sxs-lookup"><span data-stu-id="5cca6-105">You will learn how to configure single sign-on to Google Apps, how to enable automated user provisioning, and how to assign users to have access to Google Apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5cca6-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5cca6-106">Prerequisites</span></span>
1. <span data-ttu-id="5cca6-107">To access Azure Active Directory through the [Azure classic portal](https://manage.windowsazure.com), you must first have a valid Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5cca6-107">To access Azure Active Directory through the [Azure classic portal](https://manage.windowsazure.com), you must first have a valid Azure subscription.</span></span>
2. <span data-ttu-id="5cca6-108">You must have a valid tenant for [Google Apps for Work](https://www.google.com/work/apps/) or [Google Apps for Education](https://www.google.com/edu/products/productivity-tools/).</span><span class="sxs-lookup"><span data-stu-id="5cca6-108">You must have a valid tenant for [Google Apps for Work](https://www.google.com/work/apps/) or [Google Apps for Education](https://www.google.com/edu/products/productivity-tools/).</span></span> <span data-ttu-id="5cca6-109">You may use a free trial account for either service.</span><span class="sxs-lookup"><span data-stu-id="5cca6-109">You may use a free trial account for either service.</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="5cca6-110">Video tutorial</span><span class="sxs-lookup"><span data-stu-id="5cca6-110">Video tutorial</span></span>
<span data-ttu-id="5cca6-111">How to Enable Single Sign-On to Google Apps in 2 Minutes:</span><span class="sxs-lookup"><span data-stu-id="5cca6-111">How to Enable Single Sign-On to Google Apps in 2 Minutes:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]
> 
> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="5cca6-112">Frequently Asked Questions</span><span class="sxs-lookup"><span data-stu-id="5cca6-112">Frequently Asked Questions</span></span>
1. <span data-ttu-id="5cca6-113">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span><span class="sxs-lookup"><span data-stu-id="5cca6-113">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="5cca6-114">A: Yes, users will be able to sign into their Chromebook devices using their Azure AD credentials.</span><span class="sxs-lookup"><span data-stu-id="5cca6-114">A: Yes, users will be able to sign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="5cca6-115">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span><span class="sxs-lookup"><span data-stu-id="5cca6-115">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>
2. <span data-ttu-id="5cca6-116">**Q: If I enable single sign-on, will users be able to use their Azure AD credentials to sign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, etc?**</span><span class="sxs-lookup"><span data-stu-id="5cca6-116">**Q: If I enable single sign-on, will users be able to use their Azure AD credentials to sign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, etc?**</span></span>
   
    <span data-ttu-id="5cca6-117">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose to enable or disable for your organization.</span><span class="sxs-lookup"><span data-stu-id="5cca6-117">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose to enable or disable for your organization.</span></span>
3. <span data-ttu-id="5cca6-118">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span><span class="sxs-lookup"><span data-stu-id="5cca6-118">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span></span>
   
    <span data-ttu-id="5cca6-119">A: No, turning on single sign-on will immediately require all of your Google Apps users to authenticate with their Azure AD credentials.</span><span class="sxs-lookup"><span data-stu-id="5cca6-119">A: No, turning on single sign-on will immediately require all of your Google Apps users to authenticate with their Azure AD credentials.</span></span> <span data-ttu-id="5cca6-120">Because Google Apps doesn't support having multiple identity providers, the identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at the same time.</span><span class="sxs-lookup"><span data-stu-id="5cca6-120">Because Google Apps doesn't support having multiple identity providers, the identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at the same time.</span></span>
4. <span data-ttu-id="5cca6-121">**Q: If a user is signed in through Windows, will they automatically authenticate to Google Apps without getting prompted for a password?**</span><span class="sxs-lookup"><span data-stu-id="5cca6-121">**Q: If a user is signed in through Windows, will they automatically authenticate to Google Apps without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="5cca6-122">A: There are two options for enabling this scenario.</span><span class="sxs-lookup"><span data-stu-id="5cca6-122">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="5cca6-123">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5cca6-123">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span> <span data-ttu-id="5cca6-124">Alternatively, users could sign into Windows devices that are domain-joined to an on-premises Active Directory that has been enabled for single sign-on to Azure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span><span class="sxs-lookup"><span data-stu-id="5cca6-124">Alternatively, users could sign into Windows devices that are domain-joined to an on-premises Active Directory that has been enabled for single sign-on to Azure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="5cca6-125">Of course, both options require that you follow the tutorial below to enable single sign-on between Azure AD and Google Apps.</span><span class="sxs-lookup"><span data-stu-id="5cca6-125">Of course, both options require that you follow the tutorial below to enable single sign-on between Azure AD and Google Apps.</span></span>

## <a name="step-1-add-google-apps-to-your-directory"></a><span data-ttu-id="5cca6-126">Step 1: Add Google Apps to your Directory</span><span class="sxs-lookup"><span data-stu-id="5cca6-126">Step 1: Add Google Apps to your Directory</span></span>
1. <span data-ttu-id="5cca6-127">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-127">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Select Active Directory from the left navigation pane.][0]
2. <span data-ttu-id="5cca6-129">From the **Directory** list, select the directory that you would like to add Google Apps to.</span><span class="sxs-lookup"><span data-stu-id="5cca6-129">From the **Directory** list, select the directory that you would like to add Google Apps to.</span></span>
3. <span data-ttu-id="5cca6-130">Click on **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="5cca6-130">Click on **Applications** in the top menu.</span></span>
   
    ![Click on Applications.][1]
4. <span data-ttu-id="5cca6-132">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="5cca6-132">Click **Add** at the bottom of the page.</span></span>
   
    ![Click Add to add a new application.][2]
5. <span data-ttu-id="5cca6-134">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-134">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Click Add an application from the gallery.][3]
6. <span data-ttu-id="5cca6-136">In the **search box**, type **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-136">In the **search box**, type **Google Apps**.</span></span> <span data-ttu-id="5cca6-137">Then select **Google Apps** from the results, and click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="5cca6-137">Then select **Google Apps** from the results, and click **Complete** to add the application.</span></span>
   
    ![Add Google Apps.][4]
7. <span data-ttu-id="5cca6-139">You should now see the Quick Start page for Google Apps:</span><span class="sxs-lookup"><span data-stu-id="5cca6-139">You should now see the Quick Start page for Google Apps:</span></span>
   
    ![Google Apps' Quick Start page in Azure AD][5]

## <a name="step-2-enable-single-sign-on"></a><span data-ttu-id="5cca6-141">Step 2: Enable Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5cca6-141">Step 2: Enable Single Sign-On</span></span>
1. <span data-ttu-id="5cca6-142">In Azure AD, on the Quick Start page for Google Apps, click the **Configure single sign-on** button.</span><span class="sxs-lookup"><span data-stu-id="5cca6-142">In Azure AD, on the Quick Start page for Google Apps, click the **Configure single sign-on** button.</span></span>
   
    ![The configure single sign-on button][6]
2. <span data-ttu-id="5cca6-144">A dialog will open and you'll see a screen that asks "How would you like users to sign on to Google Apps?"</span><span class="sxs-lookup"><span data-stu-id="5cca6-144">A dialog will open and you'll see a screen that asks "How would you like users to sign on to Google Apps?"</span></span> <span data-ttu-id="5cca6-145">Select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-145">Select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Select Azure AD Single Sign-On][7]
   
   > [!NOTE]
   > <span data-ttu-id="5cca6-147">To learn more about about the different single sign-on options, [click here](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)</span><span class="sxs-lookup"><span data-stu-id="5cca6-147">To learn more about about the different single sign-on options, [click here](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)</span></span>
   > 
   > 
3. <span data-ttu-id="5cca6-148">On the **Configure App Settings** page, for the **Sign On URL** field, type in your Google Apps tenant URL using the following format: `https://mail.google.com/a/<yourdomain>`</span><span class="sxs-lookup"><span data-stu-id="5cca6-148">On the **Configure App Settings** page, for the **Sign On URL** field, type in your Google Apps tenant URL using the following format: `https://mail.google.com/a/<yourdomain>`</span></span>
   
    ![Type in your tenant URL][8]
4. <span data-ttu-id="5cca6-150">On the **Auto configure single sign-on** page, type in the domain for your Google Apps tenant.</span><span class="sxs-lookup"><span data-stu-id="5cca6-150">On the **Auto configure single sign-on** page, type in the domain for your Google Apps tenant.</span></span> <span data-ttu-id="5cca6-151">Then press the **Configure** button.</span><span class="sxs-lookup"><span data-stu-id="5cca6-151">Then press the **Configure** button.</span></span>
   
    ![Type in your domain name and press Configure.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/ga-auto-config.png)
   
   > [!NOTE]
   > <span data-ttu-id="5cca6-153">If you prefer to configure single sign-on manually, see [Optional Step: Manually Configure Single Sign-On](#optional-step-manually-configure-single-sign-on)</span><span class="sxs-lookup"><span data-stu-id="5cca6-153">If you prefer to configure single sign-on manually, see [Optional Step: Manually Configure Single Sign-On](#optional-step-manually-configure-single-sign-on)</span></span>
   > 
   > 
5. <span data-ttu-id="5cca6-154">Sign into your Google Apps admin account.</span><span class="sxs-lookup"><span data-stu-id="5cca6-154">Sign into your Google Apps admin account.</span></span> <span data-ttu-id="5cca6-155">Then click **Allow** in order to permit Azure Active Directory to make configuration changes in your Google Apps subscription.</span><span class="sxs-lookup"><span data-stu-id="5cca6-155">Then click **Allow** in order to permit Azure Active Directory to make configuration changes in your Google Apps subscription.</span></span>
   
    ![Type in your domain name and press Configure.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/ga-consent.PNG)
6. <span data-ttu-id="5cca6-157">Wait a few seconds while Azure Active Directory configures your Google Apps tenant.</span><span class="sxs-lookup"><span data-stu-id="5cca6-157">Wait a few seconds while Azure Active Directory configures your Google Apps tenant.</span></span> <span data-ttu-id="5cca6-158">Once it completes, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-158">Once it completes, click **Next**.</span></span>
7. <span data-ttu-id="5cca6-159">On the final page of the dialog, type in an email address if you would like to receive email notifications for errors and warnings related to the maintenance of this single sign-on configuration.</span><span class="sxs-lookup"><span data-stu-id="5cca6-159">On the final page of the dialog, type in an email address if you would like to receive email notifications for errors and warnings related to the maintenance of this single sign-on configuration.</span></span>
   
   ![Type in your email address.][14]
8. <span data-ttu-id="5cca6-161">Click **Complete** to close the dialog.</span><span class="sxs-lookup"><span data-stu-id="5cca6-161">Click **Complete** to close the dialog.</span></span> <span data-ttu-id="5cca6-162">To test your configuration, see the section below titled [Assign Users to Google Apps](#step-4-assign-users-to-google-apps).</span><span class="sxs-lookup"><span data-stu-id="5cca6-162">To test your configuration, see the section below titled [Assign Users to Google Apps](#step-4-assign-users-to-google-apps).</span></span>

## <a name="optional-step-manually-configure-single-sign-on"></a><span data-ttu-id="5cca6-163">Optional Step: Manually Configure Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5cca6-163">Optional Step: Manually Configure Single Sign-On</span></span>
<span data-ttu-id="5cca6-164">If you prefer to set up single sign-on manually, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="5cca6-164">If you prefer to set up single sign-on manually, complete the following steps:</span></span>

1. <span data-ttu-id="5cca6-165">In Azure AD, on the Quick Start page for Google Apps, click the **Configure single sign-on** button.</span><span class="sxs-lookup"><span data-stu-id="5cca6-165">In Azure AD, on the Quick Start page for Google Apps, click the **Configure single sign-on** button.</span></span>
   
    ![The configure single sign-on button][6]
2. <span data-ttu-id="5cca6-167">A dialog will open and you'll see a screen that asks "How would you like users to sign on to Google Apps?"</span><span class="sxs-lookup"><span data-stu-id="5cca6-167">A dialog will open and you'll see a screen that asks "How would you like users to sign on to Google Apps?"</span></span> <span data-ttu-id="5cca6-168">Select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-168">Select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Select Azure AD Single Sign-On][7]
   
   > [!NOTE]
   > <span data-ttu-id="5cca6-170">To learn more about about the different single sign-on options, [click here](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)</span><span class="sxs-lookup"><span data-stu-id="5cca6-170">To learn more about about the different single sign-on options, [click here](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)</span></span>
   > 
   > 
3. <span data-ttu-id="5cca6-171">On the **Configure App Settings** page, for the **Sign On URL** field, type in your Google Apps tenant URL using the following format: `https://mail.google.com/a/<yourdomain>`</span><span class="sxs-lookup"><span data-stu-id="5cca6-171">On the **Configure App Settings** page, for the **Sign On URL** field, type in your Google Apps tenant URL using the following format: `https://mail.google.com/a/<yourdomain>`</span></span>
   
    ![Type in your tenant URL][8]
4. <span data-ttu-id="5cca6-173">On the **Auto configure single sign-on** page, select the checkbox labeled **Manually configure this application for single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-173">On the **Auto configure single sign-on** page, select the checkbox labeled **Manually configure this application for single sign-on**.</span></span> <span data-ttu-id="5cca6-174">Then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-174">Then click **Next**.</span></span>
   
    ![Choose manual configuration.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/ga-auto-skip.PNG)
5. <span data-ttu-id="5cca6-176">On the **Configure single sign-on at Google Apps** page, click on **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="5cca6-176">On the **Configure single sign-on at Google Apps** page, click on **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![Download the certificate.][9]
6. <span data-ttu-id="5cca6-178">Open a new tab in your browser, and sign into the [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span><span class="sxs-lookup"><span data-stu-id="5cca6-178">Open a new tab in your browser, and sign into the [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span></span>
7. <span data-ttu-id="5cca6-179">Click **Security**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-179">Click **Security**.</span></span> <span data-ttu-id="5cca6-180">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="5cca6-180">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span></span>
   
    ![Click Security.][10]
8. <span data-ttu-id="5cca6-182">On the **Security** page, click **Set up single sign-on (SSO).**</span><span class="sxs-lookup"><span data-stu-id="5cca6-182">On the **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![Click SSO.][11]
9. <span data-ttu-id="5cca6-184">Perform the following configuration changes:</span><span class="sxs-lookup"><span data-stu-id="5cca6-184">Perform the following configuration changes:</span></span>
   
    ![Configure SSO][12]
   
   * <span data-ttu-id="5cca6-186">Select **Setup SSO with third party identity provider**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-186">Select **Setup SSO with third party identity provider**.</span></span>
   * <span data-ttu-id="5cca6-187">In Azure AD, copy the **Single sign-on service URL**, and paste it into the **Sign-in page URL** field in Google Apps.</span><span class="sxs-lookup"><span data-stu-id="5cca6-187">In Azure AD, copy the **Single sign-on service URL**, and paste it into the **Sign-in page URL** field in Google Apps.</span></span>
   * <span data-ttu-id="5cca6-188">In Azure AD, copy the **Single sign-out service URL**, and paste it into the **Sign-out page URL** field in Google Apps.</span><span class="sxs-lookup"><span data-stu-id="5cca6-188">In Azure AD, copy the **Single sign-out service URL**, and paste it into the **Sign-out page URL** field in Google Apps.</span></span>
   * <span data-ttu-id="5cca6-189">In Azure AD, copy the **Change password URL**, and paste it into the **Change password URL** field in Google Apps.</span><span class="sxs-lookup"><span data-stu-id="5cca6-189">In Azure AD, copy the **Change password URL**, and paste it into the **Change password URL** field in Google Apps.</span></span>
   * <span data-ttu-id="5cca6-190">In Google Apps, for the **Verification certificate**, upload the certificate that you downloaded in step #4.</span><span class="sxs-lookup"><span data-stu-id="5cca6-190">In Google Apps, for the **Verification certificate**, upload the certificate that you downloaded in step #4.</span></span>
   * <span data-ttu-id="5cca6-191">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-191">Click **Save Changes**.</span></span>
10. <span data-ttu-id="5cca6-192">In Azure AD, select the single sign-on configuration confirmation checkbox to enable the certificate that you uploaded to Google Apps.</span><span class="sxs-lookup"><span data-stu-id="5cca6-192">In Azure AD, select the single sign-on configuration confirmation checkbox to enable the certificate that you uploaded to Google Apps.</span></span> <span data-ttu-id="5cca6-193">Then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-193">Then click **Next**.</span></span>
    
     ![Check the confirmation checkbox][13]
11. <span data-ttu-id="5cca6-195">On the final page of the dialog, type in an email address if you would like to receive email notifications for errors and warnings related to the maintenance of this single sign-on configuration.</span><span class="sxs-lookup"><span data-stu-id="5cca6-195">On the final page of the dialog, type in an email address if you would like to receive email notifications for errors and warnings related to the maintenance of this single sign-on configuration.</span></span> 
    
    ![Type in your email address.][14]
12. <span data-ttu-id="5cca6-197">Click **Complete** to close the dialog.</span><span class="sxs-lookup"><span data-stu-id="5cca6-197">Click **Complete** to close the dialog.</span></span> <span data-ttu-id="5cca6-198">To test your configuration, see the section below titled [Assign Users to Google Apps](#step-4-assign-users-to-google-apps).</span><span class="sxs-lookup"><span data-stu-id="5cca6-198">To test your configuration, see the section below titled [Assign Users to Google Apps](#step-4-assign-users-to-google-apps).</span></span>

## <a name="step-3-enable-automated-user-provisioning"></a><span data-ttu-id="5cca6-199">Step 3: Enable Automated User Provisioning</span><span class="sxs-lookup"><span data-stu-id="5cca6-199">Step 3: Enable Automated User Provisioning</span></span>
> [!NOTE]
> <span data-ttu-id="5cca6-200">Another viable option for automating user provisioning to Google Apps is to use [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) which provisions your on-premises Active Directory identities to Google Apps.</span><span class="sxs-lookup"><span data-stu-id="5cca6-200">Another viable option for automating user provisioning to Google Apps is to use [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) which provisions your on-premises Active Directory identities to Google Apps.</span></span> <span data-ttu-id="5cca6-201">In contrast, the solution in this tutorial provisions your Azure Active Directory (cloud) users and mail-enabled groups to Google Apps.</span><span class="sxs-lookup"><span data-stu-id="5cca6-201">In contrast, the solution in this tutorial provisions your Azure Active Directory (cloud) users and mail-enabled groups to Google Apps.</span></span>
> 
> 

1. <span data-ttu-id="5cca6-202">Sign into the [Google Apps Admin Console](http://admin.google.com/) using your administrator account, and click **Security**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-202">Sign into the [Google Apps Admin Console](http://admin.google.com/) using your administrator account, and click **Security**.</span></span> <span data-ttu-id="5cca6-203">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="5cca6-203">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span></span>
   
    ![Click Security.][10]
2. <span data-ttu-id="5cca6-205">On the **Security** page, click **API Reference**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-205">On the **Security** page, click **API Reference**.</span></span>
   
    ![Click API Reference.][15]
3. <span data-ttu-id="5cca6-207">Select **Enable API access**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-207">Select **Enable API access**.</span></span>
   
    ![Click API Reference.][16]
   
   > [!IMPORTANT]
   > <span data-ttu-id="5cca6-209">For every user that you intend to provision to Google Apps, their username in Azure Active Directory *must* be tied to a custom domain.</span><span class="sxs-lookup"><span data-stu-id="5cca6-209">For every user that you intend to provision to Google Apps, their username in Azure Active Directory *must* be tied to a custom domain.</span></span> <span data-ttu-id="5cca6-210">For example, usernames that look like bob@contoso.onmicrosoft.com will not be accepted by Google Apps, whereas bob@contoso.com will be accepted.</span><span class="sxs-lookup"><span data-stu-id="5cca6-210">For example, usernames that look like bob@contoso.onmicrosoft.com will not be accepted by Google Apps, whereas bob@contoso.com will be accepted.</span></span> <span data-ttu-id="5cca6-211">You can change an existing user's domain by editing their properties in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5cca6-211">You can change an existing user's domain by editing their properties in Azure AD.</span></span> <span data-ttu-id="5cca6-212">Instructions for how to set a custom domain for both Azure Active Directory and Google Apps are included below.</span><span class="sxs-lookup"><span data-stu-id="5cca6-212">Instructions for how to set a custom domain for both Azure Active Directory and Google Apps are included below.</span></span>
   > 
   > 
4. <span data-ttu-id="5cca6-213">If you haven't added a custom domain name to your Azure Active Directory yet, then follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="5cca6-213">If you haven't added a custom domain name to your Azure Active Directory yet, then follow the steps below:</span></span>
   
   * <span data-ttu-id="5cca6-214">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-214">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span> <span data-ttu-id="5cca6-215">In the directory list, select your directory.</span><span class="sxs-lookup"><span data-stu-id="5cca6-215">In the directory list, select your directory.</span></span> 
   * <span data-ttu-id="5cca6-216">Click on **Domains** from the top-level menu, and then click on **Add a custom domain**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-216">Click on **Domains** from the top-level menu, and then click on **Add a custom domain**.</span></span>
     
       ![Add a Custom Domain][17]
   * <span data-ttu-id="5cca6-218">Type your domain name into the **Domain name** field.</span><span class="sxs-lookup"><span data-stu-id="5cca6-218">Type your domain name into the **Domain name** field.</span></span> <span data-ttu-id="5cca6-219">This should be the same domain name that you intend to use for Google Apps.</span><span class="sxs-lookup"><span data-stu-id="5cca6-219">This should be the same domain name that you intend to use for Google Apps.</span></span> <span data-ttu-id="5cca6-220">When ready, click the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="5cca6-220">When ready, click the **Add** button.</span></span>
     
       ![Type in your domain name.][18]
   * <span data-ttu-id="5cca6-222">Click **Next** to go to the verification page.</span><span class="sxs-lookup"><span data-stu-id="5cca6-222">Click **Next** to go to the verification page.</span></span> <span data-ttu-id="5cca6-223">To verify that you own this domain, you must edit the domain's DNS records according to the values provided on this page.</span><span class="sxs-lookup"><span data-stu-id="5cca6-223">To verify that you own this domain, you must edit the domain's DNS records according to the values provided on this page.</span></span> <span data-ttu-id="5cca6-224">You may choose to verify using either **MX records** or **TXT records**, depending on what you select for the **Record Type** option.</span><span class="sxs-lookup"><span data-stu-id="5cca6-224">You may choose to verify using either **MX records** or **TXT records**, depending on what you select for the **Record Type** option.</span></span> <span data-ttu-id="5cca6-225">For more comprehensive instructions on how to verify domain name with Azure AD, see [Add your own domain name to Azure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="5cca6-225">For more comprehensive instructions on how to verify domain name with Azure AD, see [Add your own domain name to Azure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span></span>
     
       ![Verify your domain name.][19]
   * <span data-ttu-id="5cca6-227">Repeat the above steps for all of the domains that you intend to add to your directory.</span><span class="sxs-lookup"><span data-stu-id="5cca6-227">Repeat the above steps for all of the domains that you intend to add to your directory.</span></span>
5. <span data-ttu-id="5cca6-228">Now that you have verified all of your domains with Azure AD, you must now verify them again with Google Apps.</span><span class="sxs-lookup"><span data-stu-id="5cca6-228">Now that you have verified all of your domains with Azure AD, you must now verify them again with Google Apps.</span></span> <span data-ttu-id="5cca6-229">For each domain that isn't already registered with Google Apps, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5cca6-229">For each domain that isn't already registered with Google Apps, perform the following steps:</span></span>
   
   * <span data-ttu-id="5cca6-230">In the [Google Apps Admin Console](http://admin.google.com/), click on **Domains**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-230">In the [Google Apps Admin Console](http://admin.google.com/), click on **Domains**.</span></span>
     
       ![Click on Domains][20]
   * <span data-ttu-id="5cca6-232">Click **Add a domain or a domain alias**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-232">Click **Add a domain or a domain alias**.</span></span>
     
       ![Add a new domain][21]
   * <span data-ttu-id="5cca6-234">Select **Add another domain**, and type in the name of the domain that you would like to add.</span><span class="sxs-lookup"><span data-stu-id="5cca6-234">Select **Add another domain**, and type in the name of the domain that you would like to add.</span></span>
     
       ![Type in your domain name][22]
   * <span data-ttu-id="5cca6-236">Click on **Continue and verify domain ownership**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-236">Click on **Continue and verify domain ownership**.</span></span> <span data-ttu-id="5cca6-237">Then follow the steps to verify that you own the domain name.</span><span class="sxs-lookup"><span data-stu-id="5cca6-237">Then follow the steps to verify that you own the domain name.</span></span> <span data-ttu-id="5cca6-238">For comprehensive instructions on how to verify your domain with Google Apps, see [Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span><span class="sxs-lookup"><span data-stu-id="5cca6-238">For comprehensive instructions on how to verify your domain with Google Apps, see [Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span></span>
   * <span data-ttu-id="5cca6-239">Repeat the above steps for any additional domains that you intend to add to Google Apps.</span><span class="sxs-lookup"><span data-stu-id="5cca6-239">Repeat the above steps for any additional domains that you intend to add to Google Apps.</span></span>
     
     > [!WARNING]
     > <span data-ttu-id="5cca6-240">If you change the primary domain for your Google Apps tenant, and if you have already configured single sign-on with Azure AD, then you will have to repeat step #3 under [Step Two: Enable Single Sign-On](#step-two-enable-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="5cca6-240">If you change the primary domain for your Google Apps tenant, and if you have already configured single sign-on with Azure AD, then you will have to repeat step #3 under [Step Two: Enable Single Sign-On](#step-two-enable-single-sign-on).</span></span>
     > 
     > 
6. <span data-ttu-id="5cca6-241">In the [Google Apps Admin Console](http://admin.google.com/), click on **Admin Roles**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-241">In the [Google Apps Admin Console](http://admin.google.com/), click on **Admin Roles**.</span></span>
   
    ![Click on Google Apps][26]
7. <span data-ttu-id="5cca6-243">Determine which admin account you would like to use to manage user provisioning.</span><span class="sxs-lookup"><span data-stu-id="5cca6-243">Determine which admin account you would like to use to manage user provisioning.</span></span> <span data-ttu-id="5cca6-244">For the **admin role** of that account, edit the **Privileges** for that role.</span><span class="sxs-lookup"><span data-stu-id="5cca6-244">For the **admin role** of that account, edit the **Privileges** for that role.</span></span> <span data-ttu-id="5cca6-245">Make sure it has all of the **Admin API Privileges** enabled so that this account can be used for provisioning.</span><span class="sxs-lookup"><span data-stu-id="5cca6-245">Make sure it has all of the **Admin API Privileges** enabled so that this account can be used for provisioning.</span></span>
   
    ![Click on Google Apps][27]
   
   > [!NOTE]
   > <span data-ttu-id="5cca6-247">If you are configuring a production environment, the best practice is to create a new admin account in Google Apps specifically for this step.</span><span class="sxs-lookup"><span data-stu-id="5cca6-247">If you are configuring a production environment, the best practice is to create a new admin account in Google Apps specifically for this step.</span></span> <span data-ttu-id="5cca6-248">These account must have an admin role associated with it that has the necessary API privileges.</span><span class="sxs-lookup"><span data-stu-id="5cca6-248">These account must have an admin role associated with it that has the necessary API privileges.</span></span>
   > 
   > 
8. <span data-ttu-id="5cca6-249">In Azure Active Directory, click on **Applications** in the top-level menu, and then click on **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-249">In Azure Active Directory, click on **Applications** in the top-level menu, and then click on **Google Apps**.</span></span>
   
    ![Click on Google Apps][23]
9. <span data-ttu-id="5cca6-251">On the Quick Start page for Google Apps, click on **Configure user provisioning**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-251">On the Quick Start page for Google Apps, click on **Configure user provisioning**.</span></span>
   
    ![Configure user provisioning][24]
10. <span data-ttu-id="5cca6-253">In the dialog that opens, click on **enable user provisioning** to authenticate into the Google Apps Admin Account that you would like to use to manage provisioning.</span><span class="sxs-lookup"><span data-stu-id="5cca6-253">In the dialog that opens, click on **enable user provisioning** to authenticate into the Google Apps Admin Account that you would like to use to manage provisioning.</span></span>
    
    ![Enable provisioning][25]
11. <span data-ttu-id="5cca6-255">Confirm that you would like to give Azure Active Directory permission to make changes to your Google Apps tenant.</span><span class="sxs-lookup"><span data-stu-id="5cca6-255">Confirm that you would like to give Azure Active Directory permission to make changes to your Google Apps tenant.</span></span>
    
    ![Confirm permissions.][28]
12. <span data-ttu-id="5cca6-257">Click **Complete** to close the dialog.</span><span class="sxs-lookup"><span data-stu-id="5cca6-257">Click **Complete** to close the dialog.</span></span>

## <a name="step-4-assign-users-to-google-apps"></a><span data-ttu-id="5cca6-258">Step 4: Assign Users to Google Apps</span><span class="sxs-lookup"><span data-stu-id="5cca6-258">Step 4: Assign Users to Google Apps</span></span>
1. <span data-ttu-id="5cca6-259">To test your configuration, start creating a new test account in the directory.</span><span class="sxs-lookup"><span data-stu-id="5cca6-259">To test your configuration, start creating a new test account in the directory.</span></span>
2. <span data-ttu-id="5cca6-260">On the Google Apps Quick Start page, click on the **Assign Users** button.</span><span class="sxs-lookup"><span data-stu-id="5cca6-260">On the Google Apps Quick Start page, click on the **Assign Users** button.</span></span>
   
    ![Click on Assign Users][29]
3. <span data-ttu-id="5cca6-262">Select your test user, and click the **Assign** button at the bottom of the screen:</span><span class="sxs-lookup"><span data-stu-id="5cca6-262">Select your test user, and click the **Assign** button at the bottom of the screen:</span></span>
   
   * <span data-ttu-id="5cca6-263">If you haven't enable automated user provisioning, then you'll see the following prompt to confirm:</span><span class="sxs-lookup"><span data-stu-id="5cca6-263">If you haven't enable automated user provisioning, then you'll see the following prompt to confirm:</span></span>
     
        ![Confirm the assignment.][30]
   * <span data-ttu-id="5cca6-265">If you have enabled automated user provisioning, then you'll see a prompt to define what type of role the user should have in Google Apps.</span><span class="sxs-lookup"><span data-stu-id="5cca6-265">If you have enabled automated user provisioning, then you'll see a prompt to define what type of role the user should have in Google Apps.</span></span> <span data-ttu-id="5cca6-266">Newly provisioned users should appear in your Google Apps environment after a few minutes.</span><span class="sxs-lookup"><span data-stu-id="5cca6-266">Newly provisioned users should appear in your Google Apps environment after a few minutes.</span></span>
4. <span data-ttu-id="5cca6-267">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into the test account, and click on **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="5cca6-267">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into the test account, and click on **Google Apps**.</span></span>

## <a name="related-articles"></a><span data-ttu-id="5cca6-268">Related Articles</span><span class="sxs-lookup"><span data-stu-id="5cca6-268">Related Articles</span></span>
* [<span data-ttu-id="5cca6-269">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5cca6-269">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="5cca6-270">List of Tutorials on How to Integrate SaaS Apps</span><span class="sxs-lookup"><span data-stu-id="5cca6-270">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/azure-active-directory.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/applications-tab.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/add-app.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/add-app-gallery.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/add-gapps.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-google-apps-tutorial/assign-confirm.png


































