---
title: 'Tutorial: Azure Active Directory integration with Questetra BPM Suite | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Questetra BPM Suite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: 655140fc7f8cc52adf6a13a99cef531f28d5cefc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866388"
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="7f30a-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="7f30a-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>

<span data-ttu-id="7f30a-104">In this tutorial, you learn how to integrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7f30a-104">In this tutorial, you learn how to integrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7f30a-105">Integrating Questetra BPM Suite with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7f30a-105">Integrating Questetra BPM Suite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7f30a-106">You can control in Azure AD who has access to Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="7f30a-106">You can control in Azure AD who has access to Questetra BPM Suite</span></span>
- <span data-ttu-id="7f30a-107">You can enable your users to automatically get signed-on to Questetra BPM Suite (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="7f30a-107">You can enable your users to automatically get signed-on to Questetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7f30a-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7f30a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7f30a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="7f30a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f30a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7f30a-110">Prerequisites</span></span>

<span data-ttu-id="7f30a-111">To configure Azure AD integration with Questetra BPM Suite, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7f30a-111">To configure Azure AD integration with Questetra BPM Suite, you need the following items:</span></span>

- <span data-ttu-id="7f30a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7f30a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7f30a-113">A Questetra BPM Suite single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7f30a-113">A Questetra BPM Suite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7f30a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7f30a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7f30a-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7f30a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7f30a-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="7f30a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7f30a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7f30a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7f30a-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7f30a-118">Scenario description</span></span>
<span data-ttu-id="7f30a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7f30a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7f30a-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7f30a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7f30a-121">Add Questetra BPM Suite from the gallery</span><span class="sxs-lookup"><span data-stu-id="7f30a-121">Add Questetra BPM Suite from the gallery</span></span>
1. <span data-ttu-id="7f30a-122">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7f30a-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-questetra-bpm-suite-from-the-gallery"></a><span data-ttu-id="7f30a-123">Add Questetra BPM Suite from the gallery</span><span class="sxs-lookup"><span data-stu-id="7f30a-123">Add Questetra BPM Suite from the gallery</span></span>
<span data-ttu-id="7f30a-124">To configure the integration of Questetra BPM Suite into Azure AD, you need to add Questetra BPM Suite from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7f30a-124">To configure the integration of Questetra BPM Suite into Azure AD, you need to add Questetra BPM Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7f30a-125">**To add Questetra BPM Suite from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7f30a-125">**To add Questetra BPM Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7f30a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7f30a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="7f30a-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7f30a-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="7f30a-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="7f30a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="7f30a-133">In the search box, type **Questetra BPM Suite**, select **Questetra BPM Suite** from result panel and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="7f30a-133">In the search box, type **Questetra BPM Suite**, select **Questetra BPM Suite** from result panel and then click **Add** button to add the application.</span></span>

    ![Add from gallery](./media/questetra-bpm-suite-tutorial/tutorial_questetra-bpm-suite_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7f30a-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7f30a-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="7f30a-136">In this section, you configure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7f30a-136">In this section, you configure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7f30a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Questetra BPM Suite is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f30a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Questetra BPM Suite is to a user in Azure AD.</span></span> <span data-ttu-id="7f30a-138">In other words, a link relationship between an Azure AD user and the related user in Questetra BPM Suite needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7f30a-138">In other words, a link relationship between an Azure AD user and the related user in Questetra BPM Suite needs to be established.</span></span>

<span data-ttu-id="7f30a-139">In Questetra BPM Suite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="7f30a-139">In Questetra BPM Suite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7f30a-140">To configure and test Azure AD single sign-on with Questetra BPM Suite, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7f30a-140">To configure and test Azure AD single sign-on with Questetra BPM Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7f30a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7f30a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="7f30a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f30a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="7f30a-143">**[Create a Questetra BPM Suite test user](#create-a-questetra-bpm-suite-test-user)** - to have a counterpart of Britta Simon in Questetra BPM Suite that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="7f30a-143">**[Create a Questetra BPM Suite test user](#create-a-questetra-bpm-suite-test-user)** - to have a counterpart of Britta Simon in Questetra BPM Suite that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="7f30a-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7f30a-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="7f30a-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7f30a-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7f30a-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7f30a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7f30a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Questetra BPM Suite application.</span><span class="sxs-lookup"><span data-stu-id="7f30a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="7f30a-148">**To configure Azure AD single sign-on with Questetra BPM Suite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7f30a-148">**To configure Azure AD single sign-on with Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="7f30a-149">In the Azure portal, on the **Questetra BPM Suite** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-149">In the Azure portal, on the **Questetra BPM Suite** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="7f30a-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7f30a-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML-based Sign-on](./media/questetra-bpm-suite-tutorial/tutorial_questetra-bpm-suite_samlbase.png)

1. <span data-ttu-id="7f30a-153">On the **Questetra BPM Suite Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7f30a-153">On the **Questetra BPM Suite Domain and URLs** section, perform the following steps:</span></span>

    ![Questetra BPM Suite Domain and URLs section](./media/questetra-bpm-suite-tutorial/tutorial_questetra-bpm-suite_url.png)

    <span data-ttu-id="7f30a-155">a.</span><span class="sxs-lookup"><span data-stu-id="7f30a-155">a.</span></span> <span data-ttu-id="7f30a-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.questetra.net/saml/SSO/alias/bpm`</span><span class="sxs-lookup"><span data-stu-id="7f30a-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.questetra.net/saml/SSO/alias/bpm`</span></span>

    <span data-ttu-id="7f30a-157">b.</span><span class="sxs-lookup"><span data-stu-id="7f30a-157">b.</span></span> <span data-ttu-id="7f30a-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.questetra.net/`</span><span class="sxs-lookup"><span data-stu-id="7f30a-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.questetra.net/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7f30a-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="7f30a-159">These values are not real.</span></span> <span data-ttu-id="7f30a-160">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="7f30a-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7f30a-161">You can get these values from **SP Information** section on your **Questetra BPM Suite** company site, which is explained later in the tutorial or contact [Questetra BPM Suite Client support team](https://www.questetra.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="7f30a-161">You can get these values from **SP Information** section on your **Questetra BPM Suite** company site, which is explained later in the tutorial or contact [Questetra BPM Suite Client support team](https://www.questetra.com/contact/).</span></span> 
 
1. <span data-ttu-id="7f30a-162">On the **SAML Signing Certificate** section, click **Certificate (Base 64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="7f30a-162">On the **SAML Signing Certificate** section, click **Certificate (Base 64)** and then save the certificate file on your computer.</span></span>

    ![SAML Signing Certificate section](./media/questetra-bpm-suite-tutorial/tutorial_questetra-bpm-suite_certificate.png) 

1. <span data-ttu-id="7f30a-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7f30a-164">Click **Save** button.</span></span>

    ![Save Button](./media/questetra-bpm-suite-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="7f30a-166">On the **Questetra BPM Suite Configuration** section, click **Configure Questetra BPM Suite** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="7f30a-166">On the **Questetra BPM Suite Configuration** section, click **Configure Questetra BPM Suite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7f30a-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="7f30a-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Questetra BPM Suite Configuration section](./media/questetra-bpm-suite-tutorial/tutorial_questetra-bpm-suite_configure.png) 

1. <span data-ttu-id="7f30a-169">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7f30a-169">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

1. <span data-ttu-id="7f30a-170">In the menu on the top, click **System Settings**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-170">In the menu on the top, click **System Settings**.</span></span> 
   
    ![Azure AD Single Sign-On][10]

1. <span data-ttu-id="7f30a-172">To open the **SingleSignOnSAML** page, click **SSO (SAML)**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-172">To open the **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Azure AD Single Sign-On][11]

1. <span data-ttu-id="7f30a-174">On your **Questetra BPM Suite** company site, in the **SP Information** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7f30a-174">On your **Questetra BPM Suite** company site, in the **SP Information** section, perform the following steps:</span></span>

    <span data-ttu-id="7f30a-175">a.</span><span class="sxs-lookup"><span data-stu-id="7f30a-175">a.</span></span> <span data-ttu-id="7f30a-176">Copy the **ACS URL**, and then paste it into the **Sign On URL** textbox in the **Questetra BPM Suite Domain and URLs** section from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7f30a-176">Copy the **ACS URL**, and then paste it into the **Sign On URL** textbox in the **Questetra BPM Suite Domain and URLs** section from Azure portal.</span></span>
    
    <span data-ttu-id="7f30a-177">b.</span><span class="sxs-lookup"><span data-stu-id="7f30a-177">b.</span></span> <span data-ttu-id="7f30a-178">Copy the **Entity ID**, and then paste it into the **Identifier** textbox in the **Questetra BPM Suite Domain and URLs** section from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7f30a-178">Copy the **Entity ID**, and then paste it into the **Identifier** textbox in the **Questetra BPM Suite Domain and URLs** section from Azure portal.</span></span>

1. <span data-ttu-id="7f30a-179">On your **Questetra BPM Suite** company site, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7f30a-179">On your **Questetra BPM Suite** company site, perform the following steps:</span></span> 
   
    ![Configure Single Sign-On][15]
   
    <span data-ttu-id="7f30a-181">a.</span><span class="sxs-lookup"><span data-stu-id="7f30a-181">a.</span></span> <span data-ttu-id="7f30a-182">Select **Enable Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-182">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="7f30a-183">b.</span><span class="sxs-lookup"><span data-stu-id="7f30a-183">b.</span></span> <span data-ttu-id="7f30a-184">In **Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7f30a-184">In **Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="7f30a-185">c.</span><span class="sxs-lookup"><span data-stu-id="7f30a-185">c.</span></span> <span data-ttu-id="7f30a-186">In **Sign-in page URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7f30a-186">In **Sign-in page URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="7f30a-187">d.</span><span class="sxs-lookup"><span data-stu-id="7f30a-187">d.</span></span> <span data-ttu-id="7f30a-188">In **Sign-out page URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7f30a-188">In **Sign-out page URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="7f30a-189">e.</span><span class="sxs-lookup"><span data-stu-id="7f30a-189">e.</span></span> <span data-ttu-id="7f30a-190">In the **NameID format** textbox, type `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`.</span><span class="sxs-lookup"><span data-stu-id="7f30a-190">In the **NameID format** textbox, type `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`.</span></span>

    <span data-ttu-id="7f30a-191">f.</span><span class="sxs-lookup"><span data-stu-id="7f30a-191">f.</span></span> <span data-ttu-id="7f30a-192">Open your **Base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it into the **Validation certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="7f30a-192">Open your **Base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it into the **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="7f30a-193">g.</span><span class="sxs-lookup"><span data-stu-id="7f30a-193">g.</span></span> <span data-ttu-id="7f30a-194">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-194">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7f30a-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="7f30a-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7f30a-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="7f30a-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7f30a-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7f30a-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7f30a-198">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7f30a-198">Create an Azure AD test user</span></span>
<span data-ttu-id="7f30a-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f30a-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="7f30a-201">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7f30a-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7f30a-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7f30a-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/questetra-bpm-suite-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="7f30a-204">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/questetra-bpm-suite-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="7f30a-206">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="7f30a-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/questetra-bpm-suite-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="7f30a-208">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7f30a-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/questetra-bpm-suite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7f30a-210">a.</span><span class="sxs-lookup"><span data-stu-id="7f30a-210">a.</span></span> <span data-ttu-id="7f30a-211">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7f30a-212">b.</span><span class="sxs-lookup"><span data-stu-id="7f30a-212">b.</span></span> <span data-ttu-id="7f30a-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7f30a-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7f30a-214">c.</span><span class="sxs-lookup"><span data-stu-id="7f30a-214">c.</span></span> <span data-ttu-id="7f30a-215">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7f30a-216">d.</span><span class="sxs-lookup"><span data-stu-id="7f30a-216">d.</span></span> <span data-ttu-id="7f30a-217">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-217">Click **Create**.</span></span>
 
### <a name="create-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="7f30a-218">Create a Questetra BPM Suite test user</span><span class="sxs-lookup"><span data-stu-id="7f30a-218">Create a Questetra BPM Suite test user</span></span>

<span data-ttu-id="7f30a-219">The objective of this section is to create a user called Britta Simon in Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="7f30a-219">The objective of this section is to create a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="7f30a-220">**To create a user called Britta Simon in Questetra BPM Suite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7f30a-220">**To create a user called Britta Simon in Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="7f30a-221">Sign on to your Questetra BPM Suite company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7f30a-221">Sign on to your Questetra BPM Suite company site as an administrator.</span></span>
1. <span data-ttu-id="7f30a-222">Go to **System Settings > User List > New User**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-222">Go to **System Settings > User List > New User**.</span></span> 
1. <span data-ttu-id="7f30a-223">On the New User dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7f30a-223">On the New User dialog, perform the following steps:</span></span> 
   
    ![Create test user][300] 
   
    <span data-ttu-id="7f30a-225">a.</span><span class="sxs-lookup"><span data-stu-id="7f30a-225">a.</span></span> <span data-ttu-id="7f30a-226">In the **Name** textbox, type **name** of the user **britta.simon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-226">In the **Name** textbox, type **name** of the user **britta.simon@contoso.com**.</span></span>
   
    <span data-ttu-id="7f30a-227">b.</span><span class="sxs-lookup"><span data-stu-id="7f30a-227">b.</span></span> <span data-ttu-id="7f30a-228">In the **Email** textbox, type **email** of the user **britta.simon@contoso.com**</span><span class="sxs-lookup"><span data-stu-id="7f30a-228">In the **Email** textbox, type **email** of the user **britta.simon@contoso.com**</span></span>
   
    <span data-ttu-id="7f30a-229">c.</span><span class="sxs-lookup"><span data-stu-id="7f30a-229">c.</span></span> <span data-ttu-id="7f30a-230">In the **Password** textbox, type a **password** of the user.</span><span class="sxs-lookup"><span data-stu-id="7f30a-230">In the **Password** textbox, type a **password** of the user.</span></span>
    
    <span data-ttu-id="7f30a-231">d.</span><span class="sxs-lookup"><span data-stu-id="7f30a-231">d.</span></span> <span data-ttu-id="7f30a-232">Click **Add new user**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-232">Click **Add new user**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7f30a-233">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7f30a-233">Assign the Azure AD test user</span></span>

<span data-ttu-id="7f30a-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="7f30a-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Questetra BPM Suite.</span></span>

![Assign User][200] 

<span data-ttu-id="7f30a-236">**To assign Britta Simon to Questetra BPM Suite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7f30a-236">**To assign Britta Simon to Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="7f30a-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="7f30a-239">In the applications list, select **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-239">In the applications list, select **Questetra BPM Suite**.</span></span>

    ![Questetra BPM Suite in apps list](./media/questetra-bpm-suite-tutorial/tutorial_questetra-bpm-suite_app.png) 

1. <span data-ttu-id="7f30a-241">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="7f30a-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="7f30a-243">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="7f30a-243">Click **Add** button.</span></span> <span data-ttu-id="7f30a-244">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7f30a-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="7f30a-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="7f30a-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="7f30a-247">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="7f30a-247">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="7f30a-248">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7f30a-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7f30a-249">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="7f30a-249">Test single sign-on</span></span>

<span data-ttu-id="7f30a-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7f30a-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7f30a-251">When you click the Questetra BPM Suite tile in the Access Panel, you should get automatically signed-on to your Questetra BPM Suite application.</span><span class="sxs-lookup"><span data-stu-id="7f30a-251">When you click the Questetra BPM Suite tile in the Access Panel, you should get automatically signed-on to your Questetra BPM Suite application.</span></span>
<span data-ttu-id="7f30a-252">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7f30a-252">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7f30a-253">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7f30a-253">Additional resources</span></span>

* [<span data-ttu-id="7f30a-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f30a-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="7f30a-255">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7f30a-255">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/questetra-bpm-suite-tutorial/tutorial_general_04.png
[10]: ./media/questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[15]: ./media/questetra-bpm-suite-tutorial/questera_bpm_suite_08.png

[100]: ./media/questetra-bpm-suite-tutorial/tutorial_general_100.png

[200]: ./media/questetra-bpm-suite-tutorial/tutorial_general_200.png
[201]: ./media/questetra-bpm-suite-tutorial/tutorial_general_201.png
[202]: ./media/questetra-bpm-suite-tutorial/tutorial_general_202.png
[203]: ./media/questetra-bpm-suite-tutorial/tutorial_general_203.png
[300]: ./media/questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 

