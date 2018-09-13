---
title: 'Tutorial: Azure Active Directory integration with Adobe Experience Manager | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Adobe Experience Manager.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 88a95bb5-c17c-474f-bb92-1f80f5344b5a
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2017
ms.author: jeedes
ms.openlocfilehash: 56b392e57809cea0ae93800df39bb9dacd164ce2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869796"
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-experience-manager"></a><span data-ttu-id="df991-103">Tutorial: Azure Active Directory integration with Adobe Experience Manager</span><span class="sxs-lookup"><span data-stu-id="df991-103">Tutorial: Azure Active Directory integration with Adobe Experience Manager</span></span>

<span data-ttu-id="df991-104">In this tutorial, you learn how to integrate Adobe Experience Manager with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="df991-104">In this tutorial, you learn how to integrate Adobe Experience Manager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="df991-105">Integrating Adobe Experience Manager with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="df991-105">Integrating Adobe Experience Manager with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="df991-106">You can control in Azure AD who has access to Adobe Experience Manager.</span><span class="sxs-lookup"><span data-stu-id="df991-106">You can control in Azure AD who has access to Adobe Experience Manager.</span></span>
- <span data-ttu-id="df991-107">You can enable your users to automatically get signed in to Adobe Experience Manager with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="df991-107">You can enable your users to automatically get signed in to Adobe Experience Manager with their Azure AD accounts.</span></span>
- <span data-ttu-id="df991-108">You can manage your accounts in one central location--the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="df991-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="df991-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="df991-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df991-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="df991-110">Prerequisites</span></span>

<span data-ttu-id="df991-111">To configure Azure AD integration with Adobe Experience Manager, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="df991-111">To configure Azure AD integration with Adobe Experience Manager, you need the following items:</span></span>

- <span data-ttu-id="df991-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="df991-112">An Azure AD subscription</span></span>
- <span data-ttu-id="df991-113">An Adobe Experience Manager single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="df991-113">An Adobe Experience Manager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="df991-114">We don't recommend using a production environment to test the steps in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="df991-114">We don't recommend using a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="df991-115">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="df991-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="df991-116">Don't use your production environment unless it's necessary.</span><span class="sxs-lookup"><span data-stu-id="df991-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="df991-117">If you don't have an Azure AD trial environment, [get a free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="df991-117">If you don't have an Azure AD trial environment, [get a free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="df991-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="df991-118">Scenario description</span></span>
<span data-ttu-id="df991-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="df991-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="df991-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="df991-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="df991-121">Adding Adobe Experience Manager from the gallery</span><span class="sxs-lookup"><span data-stu-id="df991-121">Adding Adobe Experience Manager from the gallery</span></span>
2. <span data-ttu-id="df991-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="df991-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-adobe-experience-manager-from-the-gallery"></a><span data-ttu-id="df991-123">Add Adobe Experience Manager from the gallery</span><span class="sxs-lookup"><span data-stu-id="df991-123">Add Adobe Experience Manager from the gallery</span></span>
<span data-ttu-id="df991-124">To configure the integration of Adobe Experience Manager into Azure AD, you need to add Adobe Experience Manager from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="df991-124">To configure the integration of Adobe Experience Manager into Azure AD, you need to add Adobe Experience Manager from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="df991-125">**To add Adobe Experience Manager from the gallery, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="df991-125">**To add Adobe Experience Manager from the gallery, take the following steps:**</span></span>

1. <span data-ttu-id="df991-126">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="df991-126">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="df991-128">Go to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="df991-128">Go to **Enterprise applications**.</span></span> <span data-ttu-id="df991-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="df991-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="df991-131">To add a new application, select the **New application** button on the top of the dialog box.</span><span class="sxs-lookup"><span data-stu-id="df991-131">To add a new application, select the **New application** button on the top of the dialog box.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="df991-133">In the search box, type **Adobe Experience Manager**.</span><span class="sxs-lookup"><span data-stu-id="df991-133">In the search box, type **Adobe Experience Manager**.</span></span> <span data-ttu-id="df991-134">Select **Adobe Experience Manager** from the results panel, and then select the **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="df991-134">Select **Adobe Experience Manager** from the results panel, and then select the **Add** button to add the application.</span></span>

    ![Adobe Experience Manager in the results list](./media/adobeexperiencemanager-tutorial/tutorial_adobeexperiencemanager_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="df991-136">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="df991-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="df991-137">In this section, you configure and test Azure AD single sign-on with Adobe Experience Manager based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="df991-137">In this section, you configure and test Azure AD single sign-on with Adobe Experience Manager based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="df991-138">For single sign-on to work, Azure AD needs to know who the counterpart user in Adobe Experience Manager is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df991-138">For single sign-on to work, Azure AD needs to know who the counterpart user in Adobe Experience Manager is to a user in Azure AD.</span></span> <span data-ttu-id="df991-139">In other words, you need to establish a link between an Azure AD user and the related user in Adobe Experience Manager.</span><span class="sxs-lookup"><span data-stu-id="df991-139">In other words, you need to establish a link between an Azure AD user and the related user in Adobe Experience Manager.</span></span>

<span data-ttu-id="df991-140">In Adobe Experience Manager, give the value **Username** the same value of the **user name** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df991-140">In Adobe Experience Manager, give the value **Username** the same value of the **user name** in Azure AD.</span></span> <span data-ttu-id="df991-141">Now you have established the link between the two users.</span><span class="sxs-lookup"><span data-stu-id="df991-141">Now you have established the link between the two users.</span></span> 

<span data-ttu-id="df991-142">To configure and test Azure AD single sign-on with Adobe Experience Manager, complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="df991-142">To configure and test Azure AD single sign-on with Adobe Experience Manager, complete the following building blocks:</span></span>

1. <span data-ttu-id="df991-143">[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on) to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="df991-143">[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on) to enable your users to use this feature.</span></span>
2. <span data-ttu-id="df991-144">[Create an Azure AD test user](#create-an-azure-ad-test-user) to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df991-144">[Create an Azure AD test user](#create-an-azure-ad-test-user) to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="df991-145">[Create an Adobe Experience Manager test user](#create-an-adobe-experience-manager-test-user) to have a counterpart of Britta Simon in Adobe Experience Manager that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="df991-145">[Create an Adobe Experience Manager test user](#create-an-adobe-experience-manager-test-user) to have a counterpart of Britta Simon in Adobe Experience Manager that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="df991-146">[Assign the Azure AD test user](#assign-the-azure-ad-test-user) to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="df991-146">[Assign the Azure AD test user](#assign-the-azure-ad-test-user) to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="df991-147">[Test single sign-on](#test-single-sign-on) to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="df991-147">[Test single sign-on](#test-single-sign-on) to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="df991-148">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="df991-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="df991-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adobe Experience Manager application.</span><span class="sxs-lookup"><span data-stu-id="df991-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adobe Experience Manager application.</span></span>

<span data-ttu-id="df991-150">**To configure Azure AD single sign-on with Adobe Experience Manager, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="df991-150">**To configure Azure AD single sign-on with Adobe Experience Manager, take the following steps:**</span></span>

1. <span data-ttu-id="df991-151">In the Azure portal, on the **Adobe Experience Manager** application integration page, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="df991-151">In the Azure portal, on the **Adobe Experience Manager** application integration page, select **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="df991-153">To enable single sign-on, in the **Single sign-on** dialog box, in the **Mode** drop-down menu, select **SAML-based Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="df991-153">To enable single sign-on, in the **Single sign-on** dialog box, in the **Mode** drop-down menu, select **SAML-based Sign-on**.</span></span>
 
    ![Single sign-on dialog box](./media/adobeexperiencemanager-tutorial/tutorial_adobeexperiencemanager_samlbase.png)

3. <span data-ttu-id="df991-155">In the **Adobe Experience Manager Domain and URLs** section, take the following steps if you want to configure the app in **IdP** mode:</span><span class="sxs-lookup"><span data-stu-id="df991-155">In the **Adobe Experience Manager Domain and URLs** section, take the following steps if you want to configure the app in **IdP** mode:</span></span>

    ![Adobe Experience Manager Domain and URLs single sign-on information](./media/adobeexperiencemanager-tutorial/tutorial_adobeexperiencemanager_url1.png)

    <span data-ttu-id="df991-157">a.</span><span class="sxs-lookup"><span data-stu-id="df991-157">a.</span></span> <span data-ttu-id="df991-158">In the **Identifier** box, type a unique value that you define on your AEM server as well.</span><span class="sxs-lookup"><span data-stu-id="df991-158">In the **Identifier** box, type a unique value that you define on your AEM server as well.</span></span> 

    <span data-ttu-id="df991-159">b.</span><span class="sxs-lookup"><span data-stu-id="df991-159">b.</span></span> <span data-ttu-id="df991-160">In the **Reply URL** box, type a URL with the following pattern: `https://<AEM Server Url>/saml_login`.</span><span class="sxs-lookup"><span data-stu-id="df991-160">In the **Reply URL** box, type a URL with the following pattern: `https://<AEM Server Url>/saml_login`.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="df991-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="df991-161">These values are not real.</span></span> <span data-ttu-id="df991-162">Update these values with the actual identifier and reply URL.</span><span class="sxs-lookup"><span data-stu-id="df991-162">Update these values with the actual identifier and reply URL.</span></span> <span data-ttu-id="df991-163">To get these values, contact the [Adobe Experience Manager support team](https://helpx.adobe.com/support/experience-manager.html).</span><span class="sxs-lookup"><span data-stu-id="df991-163">To get these values, contact the [Adobe Experience Manager support team](https://helpx.adobe.com/support/experience-manager.html).</span></span>
 
4. <span data-ttu-id="df991-164">Check **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="df991-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="df991-165">Then take the following steps if you want to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="df991-165">Then take the following steps if you want to configure the application in **SP** initiated mode:</span></span>

    ![Adobe Experience Manager Domain and URLs single sign-on information](./media/adobeexperiencemanager-tutorial/tutorial_adobeexperiencemanager_spconfigure.png)

    <span data-ttu-id="df991-167">In the **Sign On URL** box, type your Adobe Experience Manager server URL.</span><span class="sxs-lookup"><span data-stu-id="df991-167">In the **Sign On URL** box, type your Adobe Experience Manager server URL.</span></span> 

5. <span data-ttu-id="df991-168">In the **SAML Signing Certificate** section, select **Certificate (Base64)**.</span><span class="sxs-lookup"><span data-stu-id="df991-168">In the **SAML Signing Certificate** section, select **Certificate (Base64)**.</span></span> <span data-ttu-id="df991-169">Then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="df991-169">Then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/adobeexperiencemanager-tutorial/tutorial_adobeexperiencemanager_certificate.png) 

6. <span data-ttu-id="df991-171">To open the configuration sign-on window in the Adobe Experience Manager Configuration section,  select **Configure Adobe Experience Manager**.</span><span class="sxs-lookup"><span data-stu-id="df991-171">To open the configuration sign-on window in the Adobe Experience Manager Configuration section,  select **Configure Adobe Experience Manager**.</span></span> <span data-ttu-id="df991-172">Copy the **SAML Sign-On Service URL**, **SAML Entity ID**, and **Sign-Out ID** from the Quick Reference section.</span><span class="sxs-lookup"><span data-stu-id="df991-172">Copy the **SAML Sign-On Service URL**, **SAML Entity ID**, and **Sign-Out ID** from the Quick Reference section.</span></span>

    ![Configuration section link](./media/adobeexperiencemanager-tutorial/tutorial_adobeexperiencemanager_configure.png) 

7. <span data-ttu-id="df991-174">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="df991-174">Select **Save**.</span></span>

    ![Configure single sign-on save button](./media/adobeexperiencemanager-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="df991-176">In another browser window, open the **Adobe Experience Manager** admin portal.</span><span class="sxs-lookup"><span data-stu-id="df991-176">In another browser window, open the **Adobe Experience Manager** admin portal.</span></span>

9. <span data-ttu-id="df991-177">Select **Settings** > **Security** > **Users**.</span><span class="sxs-lookup"><span data-stu-id="df991-177">Select **Settings** > **Security** > **Users**.</span></span>

    ![Configure the single sign-on save button](./media/adobeexperiencemanager-tutorial/tutorial_adobeexperiencemanager_user.png)

10. <span data-ttu-id="df991-179">Select **Administrator** or any other relevant user.</span><span class="sxs-lookup"><span data-stu-id="df991-179">Select **Administrator** or any other relevant user.</span></span>

    ![Configure Single Sign-On Save button](./media/adobeexperiencemanager-tutorial/tutorial_adobeexperiencemanager_admin6.png)

11. <span data-ttu-id="df991-181">Select **Account settings** > **Manage TrustStore**.</span><span class="sxs-lookup"><span data-stu-id="df991-181">Select **Account settings** > **Manage TrustStore**.</span></span>

    ![Configure Single Sign-On Save button](./media/adobeexperiencemanager-tutorial/tutorial_adobeexperiencemanager_managetrust.png)

12. <span data-ttu-id="df991-183">Under **Add Certificate from CER file**, click **Select Certificate File**.</span><span class="sxs-lookup"><span data-stu-id="df991-183">Under **Add Certificate from CER file**, click **Select Certificate File**.</span></span> <span data-ttu-id="df991-184">Browse to and select the certificate file, which you already downloaded from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="df991-184">Browse to and select the certificate file, which you already downloaded from the Azure portal.</span></span>

    ![Configure single sign-on save button](./media/adobeexperiencemanager-tutorial/tutorial_adobeexperiencemanager_user2.png)

13. <span data-ttu-id="df991-186">The certificate is added to the TrustStore.</span><span class="sxs-lookup"><span data-stu-id="df991-186">The certificate is added to the TrustStore.</span></span> <span data-ttu-id="df991-187">Note the alias of the certificate.</span><span class="sxs-lookup"><span data-stu-id="df991-187">Note the alias of the certificate.</span></span>

    ![Configure Single Sign-On Save button](./media/adobeexperiencemanager-tutorial/tutorial_adobeexperiencemanager_admin7.png)

14. <span data-ttu-id="df991-189">On the **Users** page, select **authentication-service**.</span><span class="sxs-lookup"><span data-stu-id="df991-189">On the **Users** page, select **authentication-service**.</span></span>

    ![Configure Single Sign-On Save button](./media/adobeexperiencemanager-tutorial/tutorial_adobeexperiencemanager_admin8.png)

15. <span data-ttu-id="df991-191">Select **Account settings** > **Create/Manage KeyStore**.</span><span class="sxs-lookup"><span data-stu-id="df991-191">Select **Account settings** > **Create/Manage KeyStore**.</span></span> <span data-ttu-id="df991-192">Create KeyStore by supplying a password.</span><span class="sxs-lookup"><span data-stu-id="df991-192">Create KeyStore by supplying a password.</span></span>

    ![Configure Single Sign-On Save button](./media/adobeexperiencemanager-tutorial/tutorial_adobeexperiencemanager_admin9.png)

16. <span data-ttu-id="df991-194">Go back to the admin screen.</span><span class="sxs-lookup"><span data-stu-id="df991-194">Go back to the admin screen.</span></span> <span data-ttu-id="df991-195">Then select **Settings** > **Operations** > **Web Console**.</span><span class="sxs-lookup"><span data-stu-id="df991-195">Then select **Settings** > **Operations** > **Web Console**.</span></span>

    ![Configure Single Sign-On Save button](./media/adobeexperiencemanager-tutorial/tutorial_adobeexperiencemanager_admin1.png)

    <span data-ttu-id="df991-197">This opens the configuration page.</span><span class="sxs-lookup"><span data-stu-id="df991-197">This opens the configuration page.</span></span>

    ![Configure the single sign-on save button](./media/adobeexperiencemanager-tutorial/tutorial_adobeexperiencemanager_admin2.png)

17. <span data-ttu-id="df991-199">Find **Adobe Granite SAML 2.0 Authentication Handler**.</span><span class="sxs-lookup"><span data-stu-id="df991-199">Find **Adobe Granite SAML 2.0 Authentication Handler**.</span></span> <span data-ttu-id="df991-200">Then select the **Add** icon.</span><span class="sxs-lookup"><span data-stu-id="df991-200">Then select the **Add** icon.</span></span>

    ![Configure Single Sign-On Save button](./media/adobeexperiencemanager-tutorial/tutorial_adobeexperiencemanager_admin3.png)

19. <span data-ttu-id="df991-202">Take the following actions on this page.</span><span class="sxs-lookup"><span data-stu-id="df991-202">Take the following actions on this page.</span></span>

    ![Configure Single Sign-On Save button](./media/adobeexperiencemanager-tutorial/tutorial_adobeexperiencemanager_admin4.png)

    <span data-ttu-id="df991-204">a.</span><span class="sxs-lookup"><span data-stu-id="df991-204">a.</span></span> <span data-ttu-id="df991-205">In the **Path** box, enter **/**.</span><span class="sxs-lookup"><span data-stu-id="df991-205">In the **Path** box, enter **/**.</span></span>

    <span data-ttu-id="df991-206">b.</span><span class="sxs-lookup"><span data-stu-id="df991-206">b.</span></span> <span data-ttu-id="df991-207">In the **IDP URL** box, enter the **SAML Sign-On Service URL** value that you copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="df991-207">In the **IDP URL** box, enter the **SAML Sign-On Service URL** value that you copied from the Azure portal.</span></span>

    <span data-ttu-id="df991-208">c.</span><span class="sxs-lookup"><span data-stu-id="df991-208">c.</span></span> <span data-ttu-id="df991-209">In the **IDP Certificate Alias** box, enter the **Certificate Alias** value that you added in TrustStore.</span><span class="sxs-lookup"><span data-stu-id="df991-209">In the **IDP Certificate Alias** box, enter the **Certificate Alias** value that you added in TrustStore.</span></span>

    <span data-ttu-id="df991-210">d.</span><span class="sxs-lookup"><span data-stu-id="df991-210">d.</span></span> <span data-ttu-id="df991-211">In the **Security Provided Entity ID** box, enter the unique **SAML Entity ID** value that you configured in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="df991-211">In the **Security Provided Entity ID** box, enter the unique **SAML Entity ID** value that you configured in the Azure portal.</span></span>

    <span data-ttu-id="df991-212">e.</span><span class="sxs-lookup"><span data-stu-id="df991-212">e.</span></span> <span data-ttu-id="df991-213">In the **Assertion Consumer Service URL** box, enter the **Reply URL** value that you configured in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="df991-213">In the **Assertion Consumer Service URL** box, enter the **Reply URL** value that you configured in the Azure portal.</span></span>

    <span data-ttu-id="df991-214">f.</span><span class="sxs-lookup"><span data-stu-id="df991-214">f.</span></span> <span data-ttu-id="df991-215">In the **Password of Key Store** box, enter the **Password** that you set in KeyStore.</span><span class="sxs-lookup"><span data-stu-id="df991-215">In the **Password of Key Store** box, enter the **Password** that you set in KeyStore.</span></span>

    <span data-ttu-id="df991-216">g.</span><span class="sxs-lookup"><span data-stu-id="df991-216">g.</span></span> <span data-ttu-id="df991-217">In the **User Attribute ID** box, enter the **Name ID** or another user ID that's relevant in your case.</span><span class="sxs-lookup"><span data-stu-id="df991-217">In the **User Attribute ID** box, enter the **Name ID** or another user ID that's relevant in your case.</span></span>

    <span data-ttu-id="df991-218">h.</span><span class="sxs-lookup"><span data-stu-id="df991-218">h.</span></span> <span data-ttu-id="df991-219">Select **Autocreate CRX Users**.</span><span class="sxs-lookup"><span data-stu-id="df991-219">Select **Autocreate CRX Users**.</span></span>

    <span data-ttu-id="df991-220">i.</span><span class="sxs-lookup"><span data-stu-id="df991-220">i.</span></span> <span data-ttu-id="df991-221">In the **Logout URL** box, enter the unique **Sign-Out URL** value that you got from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="df991-221">In the **Logout URL** box, enter the unique **Sign-Out URL** value that you got from the Azure portal.</span></span>

    <span data-ttu-id="df991-222">j.</span><span class="sxs-lookup"><span data-stu-id="df991-222">j.</span></span> <span data-ttu-id="df991-223">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="df991-223">Select **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="df991-224">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com) while you are setting up the app.</span><span class="sxs-lookup"><span data-stu-id="df991-224">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com) while you are setting up the app.</span></span> <span data-ttu-id="df991-225">After you add this app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab. Then access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="df991-225">After you add this app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab. Then access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="df991-226">You can read more about the embedded documentation feature at [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="df991-226">You can read more about the embedded documentation feature at [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="df991-227">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="df991-227">Create an Azure AD test user</span></span>

<span data-ttu-id="df991-228">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df991-228">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="df991-230">**To create a test user in Azure AD, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="df991-230">**To create a test user in Azure AD, take the following steps:**</span></span>

1. <span data-ttu-id="df991-231">In the Azure portal, in the left pane, select the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="df991-231">In the Azure portal, in the left pane, select the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/adobeexperiencemanager-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="df991-233">To display the list of users, go to **Users and groups**, and then select **All users**.</span><span class="sxs-lookup"><span data-stu-id="df991-233">To display the list of users, go to **Users and groups**, and then select **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/adobeexperiencemanager-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="df991-235">To open the **User** dialog box, at the top of the **All Users** dialog box, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="df991-235">To open the **User** dialog box, at the top of the **All Users** dialog box, select **Add**.</span></span>

    ![The Add button](./media/adobeexperiencemanager-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="df991-237">In the **User** dialog box, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="df991-237">In the **User** dialog box, take the following steps:</span></span>

    ![The User dialog box](./media/adobeexperiencemanager-tutorial/create_aaduser_04.png)

    <span data-ttu-id="df991-239">a.</span><span class="sxs-lookup"><span data-stu-id="df991-239">a.</span></span> <span data-ttu-id="df991-240">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="df991-240">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="df991-241">b.</span><span class="sxs-lookup"><span data-stu-id="df991-241">b.</span></span> <span data-ttu-id="df991-242">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df991-242">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="df991-243">c.</span><span class="sxs-lookup"><span data-stu-id="df991-243">c.</span></span> <span data-ttu-id="df991-244">Select the **Show Password** check box.</span><span class="sxs-lookup"><span data-stu-id="df991-244">Select the **Show Password** check box.</span></span> <span data-ttu-id="df991-245">Then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="df991-245">Then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="df991-246">d.</span><span class="sxs-lookup"><span data-stu-id="df991-246">d.</span></span> <span data-ttu-id="df991-247">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="df991-247">Select **Create**.</span></span>
  
### <a name="create-an-adobe-experience-manager-test-user"></a><span data-ttu-id="df991-248">Create an Adobe Experience Manager test user</span><span class="sxs-lookup"><span data-stu-id="df991-248">Create an Adobe Experience Manager test user</span></span>

<span data-ttu-id="df991-249">In this section, you create a user called Britta Simon in Adobe Experience Manager.</span><span class="sxs-lookup"><span data-stu-id="df991-249">In this section, you create a user called Britta Simon in Adobe Experience Manager.</span></span> <span data-ttu-id="df991-250">If you selected the **Autocreate CRX Users** option, users are created automatically after successful authentication.</span><span class="sxs-lookup"><span data-stu-id="df991-250">If you selected the **Autocreate CRX Users** option, users are created automatically after successful authentication.</span></span> 

<span data-ttu-id="df991-251">If you want to create users manually, work with the [Adobe Experience Manager support team](https://helpx.adobe.com/support/experience-manager.html) to add the users in the Adobe Experience Manager platform.</span><span class="sxs-lookup"><span data-stu-id="df991-251">If you want to create users manually, work with the [Adobe Experience Manager support team](https://helpx.adobe.com/support/experience-manager.html) to add the users in the Adobe Experience Manager platform.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="df991-252">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="df991-252">Assign the Azure AD test user</span></span>

<span data-ttu-id="df991-253">In this section, you enable Britta Simon to use Azure single sign-on by granting them access to Adobe Experience Manager.</span><span class="sxs-lookup"><span data-stu-id="df991-253">In this section, you enable Britta Simon to use Azure single sign-on by granting them access to Adobe Experience Manager.</span></span>

![Assign the user role][200] 

<span data-ttu-id="df991-255">**To assign Britta Simon to Adobe Experience Manager, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="df991-255">**To assign Britta Simon to Adobe Experience Manager, take the following steps:**</span></span>

1. <span data-ttu-id="df991-256">In the Azure portal, open the applications view.</span><span class="sxs-lookup"><span data-stu-id="df991-256">In the Azure portal, open the applications view.</span></span> <span data-ttu-id="df991-257">Next, go to the directory view, select **Enterprise applications**, and then select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="df991-257">Next, go to the directory view, select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="df991-259">In the applications list, select **Adobe Experience Manager**.</span><span class="sxs-lookup"><span data-stu-id="df991-259">In the applications list, select **Adobe Experience Manager**.</span></span>

    ![The Adobe Experience Manager link in the Applications list](./media/adobeexperiencemanager-tutorial/tutorial_adobeexperiencemanager_app.png)  

3. <span data-ttu-id="df991-261">In the menu on the left, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="df991-261">In the menu on the left, select **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="df991-263">Select the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="df991-263">Select the **Add** button.</span></span> <span data-ttu-id="df991-264">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="df991-264">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="df991-266">In the **Users and groups** dialog box, select **Britta Simon** in the users list.</span><span class="sxs-lookup"><span data-stu-id="df991-266">In the **Users and groups** dialog box, select **Britta Simon** in the users list.</span></span>

6. <span data-ttu-id="df991-267">In the **Users and groups** dialog box, click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="df991-267">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="df991-268">In the **Add Assignment** dialog box, select the **Assign** button.</span><span class="sxs-lookup"><span data-stu-id="df991-268">In the **Add Assignment** dialog box, select the **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="df991-269">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="df991-269">Test single sign-on</span></span>

<span data-ttu-id="df991-270">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span><span class="sxs-lookup"><span data-stu-id="df991-270">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span></span>

<span data-ttu-id="df991-271">When you select the Adobe Experience Manager tile in the access panel, you should get automatically signed in to your Adobe Experience Manager application.</span><span class="sxs-lookup"><span data-stu-id="df991-271">When you select the Adobe Experience Manager tile in the access panel, you should get automatically signed in to your Adobe Experience Manager application.</span></span>

<span data-ttu-id="df991-272">For more information about the access panel, see [Introduction to the access panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="df991-272">For more information about the access panel, see [Introduction to the access panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="df991-273">Additional resources</span><span class="sxs-lookup"><span data-stu-id="df991-273">Additional resources</span></span>

* [<span data-ttu-id="df991-274">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="df991-274">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="df991-275">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="df991-275">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/adobeexperiencemanager-tutorial/tutorial_general_01.png
[2]: ./media/adobeexperiencemanager-tutorial/tutorial_general_02.png
[3]: ./media/adobeexperiencemanager-tutorial/tutorial_general_03.png
[4]: ./media/adobeexperiencemanager-tutorial/tutorial_general_04.png

[100]: ./media/adobeexperiencemanager-tutorial/tutorial_general_100.png

[200]: ./media/adobeexperiencemanager-tutorial/tutorial_general_200.png
[201]: ./media/adobeexperiencemanager-tutorial/tutorial_general_201.png
[202]: ./media/adobeexperiencemanager-tutorial/tutorial_general_202.png
[203]: ./media/adobeexperiencemanager-tutorial/tutorial_general_203.png

