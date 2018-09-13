---
title: 'Tutorial: Azure Active Directory integration with Zoom | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Zoom.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0ebdab6c-83a8-4737-a86a-974f37269c31
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/28/2017
ms.author: jeedes
ms.openlocfilehash: 57ae31245a356a4cd5769fe71ef471922bf6faf9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868386"
---
# <a name="tutorial-azure-active-directory-integration-with-zoom"></a><span data-ttu-id="54848-103">Tutorial: Azure Active Directory integration with Zoom</span><span class="sxs-lookup"><span data-stu-id="54848-103">Tutorial: Azure Active Directory integration with Zoom</span></span>

<span data-ttu-id="54848-104">In this tutorial, you learn how to integrate Zoom with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="54848-104">In this tutorial, you learn how to integrate Zoom with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="54848-105">Integrating Zoom with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="54848-105">Integrating Zoom with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="54848-106">You can control in Azure AD who has access to Zoom.</span><span class="sxs-lookup"><span data-stu-id="54848-106">You can control in Azure AD who has access to Zoom.</span></span>
- <span data-ttu-id="54848-107">You can enable your users to automatically get signed-on to Zoom (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="54848-107">You can enable your users to automatically get signed-on to Zoom (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="54848-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="54848-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="54848-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="54848-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54848-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="54848-110">Prerequisites</span></span>

<span data-ttu-id="54848-111">To configure Azure AD integration with Zoom, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="54848-111">To configure Azure AD integration with Zoom, you need the following items:</span></span>

- <span data-ttu-id="54848-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="54848-112">An Azure AD subscription</span></span>
- <span data-ttu-id="54848-113">A Zoom single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="54848-113">A Zoom single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="54848-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="54848-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="54848-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="54848-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="54848-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="54848-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="54848-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="54848-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="54848-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="54848-118">Scenario description</span></span>
<span data-ttu-id="54848-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="54848-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="54848-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="54848-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="54848-121">Adding Zoom from the gallery</span><span class="sxs-lookup"><span data-stu-id="54848-121">Adding Zoom from the gallery</span></span>
1. <span data-ttu-id="54848-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="54848-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoom-from-the-gallery"></a><span data-ttu-id="54848-123">Adding Zoom from the gallery</span><span class="sxs-lookup"><span data-stu-id="54848-123">Adding Zoom from the gallery</span></span>
<span data-ttu-id="54848-124">To configure the integration of Zoom into Azure AD, you need to add Zoom from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="54848-124">To configure the integration of Zoom into Azure AD, you need to add Zoom from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="54848-125">**To add Zoom from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54848-125">**To add Zoom from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="54848-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="54848-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="54848-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="54848-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="54848-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="54848-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="54848-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="54848-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="54848-133">In the search box, type **Zoom**, select **Zoom** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="54848-133">In the search box, type **Zoom**, select **Zoom** from result panel then click **Add** button to add the application.</span></span>

    ![Zoom in the results list](./media/zoom-tutorial/tutorial_zoom_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="54848-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="54848-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="54848-136">In this section, you configure and test Azure AD single sign-on with Zoom based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="54848-136">In this section, you configure and test Azure AD single sign-on with Zoom based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="54848-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoom is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54848-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoom is to a user in Azure AD.</span></span> <span data-ttu-id="54848-138">In other words, a link relationship between an Azure AD user and the related user in Zoom needs to be established.</span><span class="sxs-lookup"><span data-stu-id="54848-138">In other words, a link relationship between an Azure AD user and the related user in Zoom needs to be established.</span></span>

<span data-ttu-id="54848-139">In Zoom, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="54848-139">In Zoom, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="54848-140">To configure and test Azure AD single sign-on with Zoom, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="54848-140">To configure and test Azure AD single sign-on with Zoom, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="54848-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="54848-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="54848-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54848-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="54848-143">**[Create a Zoom test user](#create-a-zoom-test-user)** - to have a counterpart of Britta Simon in Zoom that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="54848-143">**[Create a Zoom test user](#create-a-zoom-test-user)** - to have a counterpart of Britta Simon in Zoom that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="54848-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="54848-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="54848-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="54848-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="54848-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="54848-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="54848-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoom application.</span><span class="sxs-lookup"><span data-stu-id="54848-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoom application.</span></span>

<span data-ttu-id="54848-148">**To configure Azure AD single sign-on with Zoom, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54848-148">**To configure Azure AD single sign-on with Zoom, perform the following steps:**</span></span>

1. <span data-ttu-id="54848-149">In the Azure portal, on the **Zoom** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="54848-149">In the Azure portal, on the **Zoom** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="54848-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="54848-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/zoom-tutorial/tutorial_zoom_samlbase.png)

1. <span data-ttu-id="54848-153">On the **Zoom Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54848-153">On the **Zoom Domain and URLs** section, perform the following steps:</span></span>

    ![Zoom Domain and URLs single sign-on information](./media/zoom-tutorial/tutorial_zoom_url.png)

    <span data-ttu-id="54848-155">a.</span><span class="sxs-lookup"><span data-stu-id="54848-155">a.</span></span> <span data-ttu-id="54848-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="54848-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.zoom.us`</span></span>

    <span data-ttu-id="54848-157">b.</span><span class="sxs-lookup"><span data-stu-id="54848-157">b.</span></span> <span data-ttu-id="54848-158">In the **Identifier** textbox, type a URL using the following pattern: `<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="54848-158">In the **Identifier** textbox, type a URL using the following pattern: `<companyname>.zoom.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="54848-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="54848-159">These values are not real.</span></span> <span data-ttu-id="54848-160">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="54848-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="54848-161">Contact [Zoom Client support team](https://support.zoom.us/hc) to get these values.</span><span class="sxs-lookup"><span data-stu-id="54848-161">Contact [Zoom Client support team](https://support.zoom.us/hc) to get these values.</span></span>

1. <span data-ttu-id="54848-162">The Zoom application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="54848-162">The Zoom application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="54848-163">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="54848-163">Configure the following claims for this application.</span></span> <span data-ttu-id="54848-164">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="54848-164">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> 

    ![Configure Single Sign-On](./media/zoom-tutorial/tutorial_attribute.png)

1. <span data-ttu-id="54848-166">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54848-166">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
    
    | <span data-ttu-id="54848-167">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="54848-167">Attribute Name</span></span> | <span data-ttu-id="54848-168">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="54848-168">Attribute Value</span></span> | <span data-ttu-id="54848-169">Namespace Value</span><span class="sxs-lookup"><span data-stu-id="54848-169">Namespace Value</span></span> |
    | ------------------- | -----------|--------- |    
    | <span data-ttu-id="54848-170">Email address</span><span class="sxs-lookup"><span data-stu-id="54848-170">Email address</span></span> | <span data-ttu-id="54848-171">user.mail</span><span class="sxs-lookup"><span data-stu-id="54848-171">user.mail</span></span> | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/mail`|
    | <span data-ttu-id="54848-172">First name</span><span class="sxs-lookup"><span data-stu-id="54848-172">First name</span></span> | <span data-ttu-id="54848-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="54848-173">user.givenname</span></span> | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`|
    | <span data-ttu-id="54848-174">Last name</span><span class="sxs-lookup"><span data-stu-id="54848-174">Last name</span></span> | <span data-ttu-id="54848-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="54848-175">user.surname</span></span> | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname `|
    | <span data-ttu-id="54848-176">Phone number</span><span class="sxs-lookup"><span data-stu-id="54848-176">Phone number</span></span> | <span data-ttu-id="54848-177">user.telephonenumber</span><span class="sxs-lookup"><span data-stu-id="54848-177">user.telephonenumber</span></span> | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/phone`|
    | <span data-ttu-id="54848-178">Department</span><span class="sxs-lookup"><span data-stu-id="54848-178">Department</span></span> | <span data-ttu-id="54848-179">user.department</span><span class="sxs-lookup"><span data-stu-id="54848-179">user.department</span></span> | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/department`|

    <span data-ttu-id="54848-180">a.</span><span class="sxs-lookup"><span data-stu-id="54848-180">a.</span></span> <span data-ttu-id="54848-181">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="54848-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/zoom-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/zoom-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="54848-184">b.</span><span class="sxs-lookup"><span data-stu-id="54848-184">b.</span></span> <span data-ttu-id="54848-185">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="54848-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="54848-186">c.</span><span class="sxs-lookup"><span data-stu-id="54848-186">c.</span></span> <span data-ttu-id="54848-187">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="54848-187">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="54848-188">d.</span><span class="sxs-lookup"><span data-stu-id="54848-188">d.</span></span> <span data-ttu-id="54848-189">In the **Namespace** textbox, type the namespace value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="54848-189">In the **Namespace** textbox, type the namespace value shown for that row.</span></span>
    
    <span data-ttu-id="54848-190">e.</span><span class="sxs-lookup"><span data-stu-id="54848-190">e.</span></span> <span data-ttu-id="54848-191">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="54848-191">Click **Ok**.</span></span> 
 
1. <span data-ttu-id="54848-192">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="54848-192">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/zoom-tutorial/tutorial_zoom_certificate.png)

1. <span data-ttu-id="54848-194">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="54848-194">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/zoom-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="54848-196">On the **Zoom Configuration** section, click **Configure Zoom** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="54848-196">On the **Zoom Configuration** section, click **Configure Zoom** to open **Configure sign-on** window.</span></span> <span data-ttu-id="54848-197">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="54848-197">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Zoom Configuration](./media/zoom-tutorial/tutorial_zoom_configure.png)

1. <span data-ttu-id="54848-199">In a different web browser window, log in to your Zoom company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="54848-199">In a different web browser window, log in to your Zoom company site as an administrator.</span></span>

1. <span data-ttu-id="54848-200">Click the **Single Sign-On** tab.</span><span class="sxs-lookup"><span data-stu-id="54848-200">Click the **Single Sign-On** tab.</span></span>
   
    <span data-ttu-id="54848-201">![Single sign-on tab](./media/zoom-tutorial/IC784700.png "Single sign-on")</span><span class="sxs-lookup"><span data-stu-id="54848-201">![Single sign-on tab](./media/zoom-tutorial/IC784700.png "Single sign-on")</span></span>

1. <span data-ttu-id="54848-202">Click the **Security Control** tab, and then go to the **Single Sign-On** settings.</span><span class="sxs-lookup"><span data-stu-id="54848-202">Click the **Security Control** tab, and then go to the **Single Sign-On** settings.</span></span>

1. <span data-ttu-id="54848-203">In the Single Sign-On section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54848-203">In the Single Sign-On section, perform the following steps:</span></span>
   
    <span data-ttu-id="54848-204">![Single sign-on section](./media/zoom-tutorial/IC784701.png "Single sign-on")</span><span class="sxs-lookup"><span data-stu-id="54848-204">![Single sign-on section](./media/zoom-tutorial/IC784701.png "Single sign-on")</span></span>
   
    <span data-ttu-id="54848-205">a.</span><span class="sxs-lookup"><span data-stu-id="54848-205">a.</span></span> <span data-ttu-id="54848-206">In the **Sign-in page URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="54848-206">In the **Sign-in page URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="54848-207">b.</span><span class="sxs-lookup"><span data-stu-id="54848-207">b.</span></span> <span data-ttu-id="54848-208">In the **Sign-out page URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="54848-208">In the **Sign-out page URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
     
    <span data-ttu-id="54848-209">c.</span><span class="sxs-lookup"><span data-stu-id="54848-209">c.</span></span> <span data-ttu-id="54848-210">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="54848-210">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span></span>

    <span data-ttu-id="54848-211">d.</span><span class="sxs-lookup"><span data-stu-id="54848-211">d.</span></span> <span data-ttu-id="54848-212">In the **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="54848-212">In the **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="54848-213">e.</span><span class="sxs-lookup"><span data-stu-id="54848-213">e.</span></span> <span data-ttu-id="54848-214">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="54848-214">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="54848-215">For more information, visit the zoom documentation [https://zoomus.zendesk.com/hc/en-us/articles/115005887566](https://zoomus.zendesk.com/hc/en-us/articles/115005887566)</span><span class="sxs-lookup"><span data-stu-id="54848-215">For more information, visit the zoom documentation [https://zoomus.zendesk.com/hc/en-us/articles/115005887566](https://zoomus.zendesk.com/hc/en-us/articles/115005887566)</span></span>

> [!TIP]
> <span data-ttu-id="54848-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="54848-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="54848-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="54848-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="54848-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="54848-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="54848-219">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="54848-219">Create an Azure AD test user</span></span>

<span data-ttu-id="54848-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54848-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="54848-222">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54848-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="54848-223">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="54848-223">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/zoom-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="54848-225">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="54848-225">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/zoom-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="54848-227">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="54848-227">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/zoom-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="54848-229">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54848-229">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/zoom-tutorial/create_aaduser_04.png)

    <span data-ttu-id="54848-231">a.</span><span class="sxs-lookup"><span data-stu-id="54848-231">a.</span></span> <span data-ttu-id="54848-232">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="54848-232">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="54848-233">b.</span><span class="sxs-lookup"><span data-stu-id="54848-233">b.</span></span> <span data-ttu-id="54848-234">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54848-234">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="54848-235">c.</span><span class="sxs-lookup"><span data-stu-id="54848-235">c.</span></span> <span data-ttu-id="54848-236">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="54848-236">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="54848-237">d.</span><span class="sxs-lookup"><span data-stu-id="54848-237">d.</span></span> <span data-ttu-id="54848-238">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="54848-238">Click **Create**.</span></span>
 
### <a name="create-a-zoom-test-user"></a><span data-ttu-id="54848-239">Create a Zoom test user</span><span class="sxs-lookup"><span data-stu-id="54848-239">Create a Zoom test user</span></span>

<span data-ttu-id="54848-240">In order to enable Azure AD users to log in to Zoom, they must be provisioned into Zoom.</span><span class="sxs-lookup"><span data-stu-id="54848-240">In order to enable Azure AD users to log in to Zoom, they must be provisioned into Zoom.</span></span> <span data-ttu-id="54848-241">In the case of Zoom, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="54848-241">In the case of Zoom, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="54848-242">To provision a user account, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54848-242">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="54848-243">Log in to your **Zoom** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="54848-243">Log in to your **Zoom** company site as an administrator.</span></span>
 
1. <span data-ttu-id="54848-244">Click the **Account Management** tab, and then click **User Management**.</span><span class="sxs-lookup"><span data-stu-id="54848-244">Click the **Account Management** tab, and then click **User Management**.</span></span>

1. <span data-ttu-id="54848-245">In the User Management section, click **Add users**.</span><span class="sxs-lookup"><span data-stu-id="54848-245">In the User Management section, click **Add users**.</span></span>
   
    <span data-ttu-id="54848-246">![User management](./media/zoom-tutorial/IC784703.png "User management")</span><span class="sxs-lookup"><span data-stu-id="54848-246">![User management](./media/zoom-tutorial/IC784703.png "User management")</span></span>

1. <span data-ttu-id="54848-247">On the **Add users** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54848-247">On the **Add users** page, perform the following steps:</span></span>
   
    <span data-ttu-id="54848-248">![Add users](./media/zoom-tutorial/IC784704.png "Add users")</span><span class="sxs-lookup"><span data-stu-id="54848-248">![Add users](./media/zoom-tutorial/IC784704.png "Add users")</span></span>
   
    <span data-ttu-id="54848-249">a.</span><span class="sxs-lookup"><span data-stu-id="54848-249">a.</span></span> <span data-ttu-id="54848-250">As **User Type**, select **Basic**.</span><span class="sxs-lookup"><span data-stu-id="54848-250">As **User Type**, select **Basic**.</span></span>

    <span data-ttu-id="54848-251">b.</span><span class="sxs-lookup"><span data-stu-id="54848-251">b.</span></span> <span data-ttu-id="54848-252">In the **Emails** textbox, type the email address of a valid Azure AD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="54848-252">In the **Emails** textbox, type the email address of a valid Azure AD account you want to provision.</span></span>

    <span data-ttu-id="54848-253">c.</span><span class="sxs-lookup"><span data-stu-id="54848-253">c.</span></span> <span data-ttu-id="54848-254">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="54848-254">Click **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="54848-255">You can use any other Zoom user account creation tools or APIs provided by Zoom to provision Azure Active Directory user accounts.</span><span class="sxs-lookup"><span data-stu-id="54848-255">You can use any other Zoom user account creation tools or APIs provided by Zoom to provision Azure Active Directory user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="54848-256">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="54848-256">Assign the Azure AD test user</span></span>

<span data-ttu-id="54848-257">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoom.</span><span class="sxs-lookup"><span data-stu-id="54848-257">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoom.</span></span>

![Assign the user role][200] 

<span data-ttu-id="54848-259">**To assign Britta Simon to Zoom, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54848-259">**To assign Britta Simon to Zoom, perform the following steps:**</span></span>

1. <span data-ttu-id="54848-260">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="54848-260">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="54848-262">In the applications list, select **Zoom**.</span><span class="sxs-lookup"><span data-stu-id="54848-262">In the applications list, select **Zoom**.</span></span>

    ![The Zoom link in the Applications list](./media/zoom-tutorial/tutorial_zoom_app.png)  

1. <span data-ttu-id="54848-264">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="54848-264">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="54848-266">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="54848-266">Click **Add** button.</span></span> <span data-ttu-id="54848-267">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="54848-267">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="54848-269">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="54848-269">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="54848-270">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="54848-270">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="54848-271">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="54848-271">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="54848-272">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="54848-272">Test single sign-on</span></span>

<span data-ttu-id="54848-273">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="54848-273">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="54848-274">When you click the Zoom tile in the Access Panel, you should get automatically signed-on to your Zoom application.</span><span class="sxs-lookup"><span data-stu-id="54848-274">When you click the Zoom tile in the Access Panel, you should get automatically signed-on to your Zoom application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="54848-275">Additional resources</span><span class="sxs-lookup"><span data-stu-id="54848-275">Additional resources</span></span>

* [<span data-ttu-id="54848-276">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="54848-276">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="54848-277">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="54848-277">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/zoom-tutorial/tutorial_general_01.png
[2]: ./media/zoom-tutorial/tutorial_general_02.png
[3]: ./media/zoom-tutorial/tutorial_general_03.png
[4]: ./media/zoom-tutorial/tutorial_general_04.png

[100]: ./media/zoom-tutorial/tutorial_general_100.png

[200]: ./media/zoom-tutorial/tutorial_general_200.png
[201]: ./media/zoom-tutorial/tutorial_general_201.png
[202]: ./media/zoom-tutorial/tutorial_general_202.png
[203]: ./media/zoom-tutorial/tutorial_general_203.png

