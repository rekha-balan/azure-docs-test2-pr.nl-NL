---
title: 'Tutorial: Azure Active Directory integration with Onit | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Onit.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: bc479a28-8fcd-493f-ac53-681975a5149c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: a93acc79fc447018b5cf63b2e2456bc394c1f78e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869437"
---
# <a name="tutorial-azure-active-directory-integration-with-onit"></a><span data-ttu-id="82d46-103">Tutorial: Azure Active Directory integration with Onit</span><span class="sxs-lookup"><span data-stu-id="82d46-103">Tutorial: Azure Active Directory integration with Onit</span></span>

<span data-ttu-id="82d46-104">In this tutorial, you learn how to integrate Onit with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="82d46-104">In this tutorial, you learn how to integrate Onit with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="82d46-105">Integrating Onit with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="82d46-105">Integrating Onit with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="82d46-106">You can control in Azure AD who has access to Onit.</span><span class="sxs-lookup"><span data-stu-id="82d46-106">You can control in Azure AD who has access to Onit.</span></span>
- <span data-ttu-id="82d46-107">You can enable your users to automatically get signed-on to Onit (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="82d46-107">You can enable your users to automatically get signed-on to Onit (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="82d46-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="82d46-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="82d46-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="82d46-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82d46-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="82d46-110">Prerequisites</span></span>

<span data-ttu-id="82d46-111">To configure Azure AD integration with Onit, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="82d46-111">To configure Azure AD integration with Onit, you need the following items:</span></span>

- <span data-ttu-id="82d46-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="82d46-112">An Azure AD subscription</span></span>
- <span data-ttu-id="82d46-113">An Onit single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="82d46-113">An Onit single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="82d46-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="82d46-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="82d46-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="82d46-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="82d46-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="82d46-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="82d46-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="82d46-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="82d46-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="82d46-118">Scenario description</span></span>

<span data-ttu-id="82d46-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="82d46-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="82d46-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="82d46-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="82d46-121">Adding Onit from the gallery</span><span class="sxs-lookup"><span data-stu-id="82d46-121">Adding Onit from the gallery</span></span>
1. <span data-ttu-id="82d46-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="82d46-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-onit-from-the-gallery"></a><span data-ttu-id="82d46-123">Adding Onit from the gallery</span><span class="sxs-lookup"><span data-stu-id="82d46-123">Adding Onit from the gallery</span></span>
<span data-ttu-id="82d46-124">To configure the integration of Onit into Azure AD, you need to add Onit from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="82d46-124">To configure the integration of Onit into Azure AD, you need to add Onit from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="82d46-125">**To add Onit from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="82d46-125">**To add Onit from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="82d46-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="82d46-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="82d46-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="82d46-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="82d46-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="82d46-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="82d46-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="82d46-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="82d46-133">In the search box, type **Onit**, select **Onit** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="82d46-133">In the search box, type **Onit**, select **Onit** from result panel then click **Add** button to add the application.</span></span>

    ![Onit in the results list](./media/onit-tutorial/tutorial_onit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="82d46-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="82d46-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="82d46-136">In this section, you configure and test Azure AD single sign-on with Onit based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="82d46-136">In this section, you configure and test Azure AD single sign-on with Onit based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="82d46-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Onit is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82d46-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Onit is to a user in Azure AD.</span></span> <span data-ttu-id="82d46-138">In other words, a link relationship between an Azure AD user and the related user in Onit needs to be established.</span><span class="sxs-lookup"><span data-stu-id="82d46-138">In other words, a link relationship between an Azure AD user and the related user in Onit needs to be established.</span></span>

<span data-ttu-id="82d46-139">In Onit, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="82d46-139">In Onit, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="82d46-140">To configure and test Azure AD single sign-on with Onit, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="82d46-140">To configure and test Azure AD single sign-on with Onit, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="82d46-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="82d46-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="82d46-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="82d46-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="82d46-143">**[Create an Onit test user](#create-an-onit-test-user)** - to have a counterpart of Britta Simon in Onit that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="82d46-143">**[Create an Onit test user](#create-an-onit-test-user)** - to have a counterpart of Britta Simon in Onit that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="82d46-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="82d46-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="82d46-145">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="82d46-145">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="82d46-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="82d46-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="82d46-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Onit application.</span><span class="sxs-lookup"><span data-stu-id="82d46-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Onit application.</span></span>

<span data-ttu-id="82d46-148">**To configure Azure AD single sign-on with Onit, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="82d46-148">**To configure Azure AD single sign-on with Onit, perform the following steps:**</span></span>

1. <span data-ttu-id="82d46-149">In the Azure portal, on the **Onit** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="82d46-149">In the Azure portal, on the **Onit** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="82d46-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="82d46-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/onit-tutorial/tutorial_onit_samlbase.png)

1. <span data-ttu-id="82d46-153">On the **Onit Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="82d46-153">On the **Onit Domain and URLs** section, perform the following steps:</span></span>

    ![Onit Domain and URLs single sign-on information](./media/onit-tutorial/tutorial_onit_url.png)

    <span data-ttu-id="82d46-155">a.</span><span class="sxs-lookup"><span data-stu-id="82d46-155">a.</span></span> <span data-ttu-id="82d46-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="82d46-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub-domain>.onit.com`</span></span>

    <span data-ttu-id="82d46-157">b.</span><span class="sxs-lookup"><span data-stu-id="82d46-157">b.</span></span> <span data-ttu-id="82d46-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="82d46-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<sub-domain>.onit.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="82d46-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="82d46-159">These values are not real.</span></span> <span data-ttu-id="82d46-160">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="82d46-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="82d46-161">Contact [Onit Client support team](https://www.onit.com/support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="82d46-161">Contact [Onit Client support team](https://www.onit.com/support) to get these values.</span></span> 
 
1. <span data-ttu-id="82d46-162">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span><span class="sxs-lookup"><span data-stu-id="82d46-162">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![The Certificate download link](./media/onit-tutorial/tutorial_onit_certificate.png) 

1. <span data-ttu-id="82d46-164">Onit application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="82d46-164">Onit application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="82d46-165">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="82d46-165">Please configure the following claims for this application.</span></span> <span data-ttu-id="82d46-166">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span><span class="sxs-lookup"><span data-stu-id="82d46-166">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="82d46-167">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="82d46-167">The following screenshot shows an example for this.</span></span> 

    ![Configure Single Sign-On](./media/onit-tutorial/tutorial_onit_attribute.png) 

1. <span data-ttu-id="82d46-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="82d46-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="82d46-170">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="82d46-170">Attribute Name</span></span> | <span data-ttu-id="82d46-171">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="82d46-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="82d46-172">email</span><span class="sxs-lookup"><span data-stu-id="82d46-172">email</span></span> | <span data-ttu-id="82d46-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="82d46-173">user.mail</span></span> |
    
    <span data-ttu-id="82d46-174">a.</span><span class="sxs-lookup"><span data-stu-id="82d46-174">a.</span></span> <span data-ttu-id="82d46-175">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="82d46-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/onit-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/onit-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="82d46-178">b.</span><span class="sxs-lookup"><span data-stu-id="82d46-178">b.</span></span> <span data-ttu-id="82d46-179">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="82d46-179">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="82d46-180">c.</span><span class="sxs-lookup"><span data-stu-id="82d46-180">c.</span></span> <span data-ttu-id="82d46-181">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="82d46-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="82d46-182">d.</span><span class="sxs-lookup"><span data-stu-id="82d46-182">d.</span></span> <span data-ttu-id="82d46-183">Leave the **Namespace** blank.</span><span class="sxs-lookup"><span data-stu-id="82d46-183">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="82d46-184">e.</span><span class="sxs-lookup"><span data-stu-id="82d46-184">e.</span></span> <span data-ttu-id="82d46-185">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="82d46-185">Click **Ok**.</span></span>

1. <span data-ttu-id="82d46-186">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="82d46-186">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/onit-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="82d46-188">On the **Onit Configuration** section, click **Configure Onit** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="82d46-188">On the **Onit Configuration** section, click **Configure Onit** to open **Configure sign-on** window.</span></span> <span data-ttu-id="82d46-189">Copy the **Sign-Out URL, SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="82d46-189">Copy the **Sign-Out URL, SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Onit Configuration](./media/onit-tutorial/tutorial_onit_configure.png)

1. <span data-ttu-id="82d46-191">In a different web browser window, log into your Onit company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="82d46-191">In a different web browser window, log into your Onit company site as an administrator.</span></span>

1. <span data-ttu-id="82d46-192">In the menu on the top, click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="82d46-192">In the menu on the top, click **Administration**.</span></span>
   
   <span data-ttu-id="82d46-193">![Administration](./media/onit-tutorial/IC791174.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="82d46-193">![Administration](./media/onit-tutorial/IC791174.png "Administration")</span></span>
1. <span data-ttu-id="82d46-194">Click **Edit Corporation**.</span><span class="sxs-lookup"><span data-stu-id="82d46-194">Click **Edit Corporation**.</span></span>
   
   <span data-ttu-id="82d46-195">![Edit Corporation](./media/onit-tutorial/IC791175.png "Edit Corporation")</span><span class="sxs-lookup"><span data-stu-id="82d46-195">![Edit Corporation](./media/onit-tutorial/IC791175.png "Edit Corporation")</span></span>
   
1. <span data-ttu-id="82d46-196">Click the **Security** tab.</span><span class="sxs-lookup"><span data-stu-id="82d46-196">Click the **Security** tab.</span></span>
    
    <span data-ttu-id="82d46-197">![Edit Company Information](./media/onit-tutorial/IC791176.png "Edit Company Information")</span><span class="sxs-lookup"><span data-stu-id="82d46-197">![Edit Company Information](./media/onit-tutorial/IC791176.png "Edit Company Information")</span></span>

1. <span data-ttu-id="82d46-198">On the **Security** tab, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="82d46-198">On the **Security** tab, perform the following steps:</span></span>

    <span data-ttu-id="82d46-199">![Single Sign-On](./media/onit-tutorial/IC791177.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="82d46-199">![Single Sign-On](./media/onit-tutorial/IC791177.png "Single Sign-On")</span></span>

    <span data-ttu-id="82d46-200">a.</span><span class="sxs-lookup"><span data-stu-id="82d46-200">a.</span></span> <span data-ttu-id="82d46-201">As **Authentication Strategy**, select **Single Sign On and Password**.</span><span class="sxs-lookup"><span data-stu-id="82d46-201">As **Authentication Strategy**, select **Single Sign On and Password**.</span></span>
    
    <span data-ttu-id="82d46-202">b.</span><span class="sxs-lookup"><span data-stu-id="82d46-202">b.</span></span> <span data-ttu-id="82d46-203">In **Idp Target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="82d46-203">In **Idp Target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="82d46-204">c.</span><span class="sxs-lookup"><span data-stu-id="82d46-204">c.</span></span> <span data-ttu-id="82d46-205">In **Idp logout URL** textbox, paste the value of  **Sign-Out URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="82d46-205">In **Idp logout URL** textbox, paste the value of  **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="82d46-206">d.</span><span class="sxs-lookup"><span data-stu-id="82d46-206">d.</span></span> <span data-ttu-id="82d46-207">In **Idp Cert Fingerprint (SHA1)** textbox, paste the  **Thumbprint** value of certificate, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="82d46-207">In **Idp Cert Fingerprint (SHA1)** textbox, paste the  **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="82d46-208">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="82d46-208">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="82d46-209">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="82d46-209">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="82d46-210">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="82d46-210">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="82d46-211">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="82d46-211">Create an Azure AD test user</span></span>

<span data-ttu-id="82d46-212">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="82d46-212">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="82d46-214">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="82d46-214">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="82d46-215">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="82d46-215">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/onit-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="82d46-217">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="82d46-217">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/onit-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="82d46-219">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="82d46-219">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/onit-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="82d46-221">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="82d46-221">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/onit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="82d46-223">a.</span><span class="sxs-lookup"><span data-stu-id="82d46-223">a.</span></span> <span data-ttu-id="82d46-224">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="82d46-224">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="82d46-225">b.</span><span class="sxs-lookup"><span data-stu-id="82d46-225">b.</span></span> <span data-ttu-id="82d46-226">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="82d46-226">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="82d46-227">c.</span><span class="sxs-lookup"><span data-stu-id="82d46-227">c.</span></span> <span data-ttu-id="82d46-228">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="82d46-228">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="82d46-229">d.</span><span class="sxs-lookup"><span data-stu-id="82d46-229">d.</span></span> <span data-ttu-id="82d46-230">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="82d46-230">Click **Create**.</span></span>
 
### <a name="create-an-onit-test-user"></a><span data-ttu-id="82d46-231">Create an Onit test user</span><span class="sxs-lookup"><span data-stu-id="82d46-231">Create an Onit test user</span></span>

<span data-ttu-id="82d46-232">In order to enable Azure AD users to log into Onit, they must be provisioned into Onit.</span><span class="sxs-lookup"><span data-stu-id="82d46-232">In order to enable Azure AD users to log into Onit, they must be provisioned into Onit.</span></span>  

<span data-ttu-id="82d46-233">In the case of Onit, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="82d46-233">In the case of Onit, provisioning is a manual task.</span></span>

<span data-ttu-id="82d46-234">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="82d46-234">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="82d46-235">Sign on to your **Onit** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="82d46-235">Sign on to your **Onit** company site as an administrator.</span></span>
1. <span data-ttu-id="82d46-236">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="82d46-236">Click **Add User**.</span></span>
   
   <span data-ttu-id="82d46-237">![Administration](./media/onit-tutorial/IC791180.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="82d46-237">![Administration](./media/onit-tutorial/IC791180.png "Administration")</span></span>
1. <span data-ttu-id="82d46-238">On the **Add User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="82d46-238">On the **Add User** dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="82d46-239">![Add User](./media/onit-tutorial/IC791181.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="82d46-239">![Add User](./media/onit-tutorial/IC791181.png "Add User")</span></span>
   
  1. <span data-ttu-id="82d46-240">Type the **Name** and the **Email Address** of a valid Azure AD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="82d46-240">Type the **Name** and the **Email Address** of a valid Azure AD account you want to provision into the related textboxes.</span></span>
  1. <span data-ttu-id="82d46-241">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="82d46-241">Click **Create**.</span></span>    
   
 > [!NOTE]
 > <span data-ttu-id="82d46-242">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="82d46-242">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="82d46-243">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="82d46-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="82d46-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Onit.</span><span class="sxs-lookup"><span data-stu-id="82d46-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Onit.</span></span>

![Assign the user role][200] 

<span data-ttu-id="82d46-246">**To assign Britta Simon to Onit, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="82d46-246">**To assign Britta Simon to Onit, perform the following steps:**</span></span>

1. <span data-ttu-id="82d46-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="82d46-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="82d46-249">In the applications list, select **Onit**.</span><span class="sxs-lookup"><span data-stu-id="82d46-249">In the applications list, select **Onit**.</span></span>

    ![The Onit link in the Applications list](./media/onit-tutorial/tutorial_onit_app.png)  

1. <span data-ttu-id="82d46-251">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="82d46-251">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="82d46-253">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="82d46-253">Click **Add** button.</span></span> <span data-ttu-id="82d46-254">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="82d46-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="82d46-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="82d46-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="82d46-257">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="82d46-257">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="82d46-258">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="82d46-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="82d46-259">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="82d46-259">Test single sign-on</span></span>

<span data-ttu-id="82d46-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="82d46-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="82d46-261">When you click the Onit tile in the Access Panel, you should get automatically signed-on to your Onit application.</span><span class="sxs-lookup"><span data-stu-id="82d46-261">When you click the Onit tile in the Access Panel, you should get automatically signed-on to your Onit application.</span></span>
<span data-ttu-id="82d46-262">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="82d46-262">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="82d46-263">Additional resources</span><span class="sxs-lookup"><span data-stu-id="82d46-263">Additional resources</span></span>

* [<span data-ttu-id="82d46-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="82d46-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="82d46-265">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="82d46-265">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/onit-tutorial/tutorial_general_01.png
[2]: ./media/onit-tutorial/tutorial_general_02.png
[3]: ./media/onit-tutorial/tutorial_general_03.png
[4]: ./media/onit-tutorial/tutorial_general_04.png

[100]: ./media/onit-tutorial/tutorial_general_100.png

[200]: ./media/onit-tutorial/tutorial_general_200.png
[201]: ./media/onit-tutorial/tutorial_general_201.png
[202]: ./media/onit-tutorial/tutorial_general_202.png
[203]: ./media/onit-tutorial/tutorial_general_203.png

