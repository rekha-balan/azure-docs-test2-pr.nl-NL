---
title: 'Tutorial: Azure Active Directory integration with Zendesk | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Zendesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2018
ms.author: jeedes
ms.openlocfilehash: 9b467fa966c2a785677f47faaa4bb8bd3ed238e2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867591"
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="85289-103">Tutorial: Azure Active Directory integration with Zendesk</span><span class="sxs-lookup"><span data-stu-id="85289-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="85289-104">In this tutorial, you learn how to integrate Zendesk with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="85289-104">In this tutorial, you learn how to integrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="85289-105">Integrating Zendesk with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="85289-105">Integrating Zendesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="85289-106">You can control in Azure AD who has access to Zendesk.</span><span class="sxs-lookup"><span data-stu-id="85289-106">You can control in Azure AD who has access to Zendesk.</span></span>
- <span data-ttu-id="85289-107">You can enable your users to automatically get signed-on to Zendesk (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="85289-107">You can enable your users to automatically get signed-on to Zendesk (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="85289-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="85289-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="85289-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="85289-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85289-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="85289-110">Prerequisites</span></span>

<span data-ttu-id="85289-111">To configure Azure AD integration with Zendesk, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="85289-111">To configure Azure AD integration with Zendesk, you need the following items:</span></span>

- <span data-ttu-id="85289-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="85289-112">An Azure AD subscription</span></span>
- <span data-ttu-id="85289-113">A Zendesk single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="85289-113">A Zendesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="85289-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="85289-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="85289-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="85289-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="85289-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="85289-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="85289-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="85289-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="85289-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="85289-118">Scenario description</span></span>
<span data-ttu-id="85289-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="85289-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="85289-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="85289-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="85289-121">Adding Zendesk from the gallery</span><span class="sxs-lookup"><span data-stu-id="85289-121">Adding Zendesk from the gallery</span></span>
1. <span data-ttu-id="85289-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="85289-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zendesk-from-the-gallery"></a><span data-ttu-id="85289-123">Adding Zendesk from the gallery</span><span class="sxs-lookup"><span data-stu-id="85289-123">Adding Zendesk from the gallery</span></span>
<span data-ttu-id="85289-124">To configure the integration of Zendesk into Azure AD, you need to add Zendesk from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="85289-124">To configure the integration of Zendesk into Azure AD, you need to add Zendesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="85289-125">**To add Zendesk from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="85289-125">**To add Zendesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="85289-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="85289-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="85289-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="85289-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="85289-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="85289-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="85289-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="85289-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="85289-133">In the search box, type **Zendesk**, select **Zendesk** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="85289-133">In the search box, type **Zendesk**, select **Zendesk** from result panel then click **Add** button to add the application.</span></span>

    ![Zendesk in the results list](./media/zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="85289-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="85289-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="85289-136">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="85289-136">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="85289-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zendesk is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85289-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zendesk is to a user in Azure AD.</span></span> <span data-ttu-id="85289-138">In other words, a link relationship between an Azure AD user and the related user in Zendesk needs to be established.</span><span class="sxs-lookup"><span data-stu-id="85289-138">In other words, a link relationship between an Azure AD user and the related user in Zendesk needs to be established.</span></span>

<span data-ttu-id="85289-139">In Zendesk, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="85289-139">In Zendesk, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="85289-140">To configure and test Azure AD single sign-on with Zendesk, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="85289-140">To configure and test Azure AD single sign-on with Zendesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="85289-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="85289-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="85289-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="85289-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="85289-143">**[Create a Zendesk test user](#create-a-zendesk-test-user)** - to have a counterpart of Britta Simon in Zendesk that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="85289-143">**[Create a Zendesk test user](#create-a-zendesk-test-user)** - to have a counterpart of Britta Simon in Zendesk that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="85289-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="85289-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="85289-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="85289-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="85289-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="85289-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="85289-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zendesk application.</span><span class="sxs-lookup"><span data-stu-id="85289-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="85289-148">**To configure Azure AD single sign-on with Zendesk, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="85289-148">**To configure Azure AD single sign-on with Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="85289-149">In the Azure portal, on the **Zendesk** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="85289-149">In the Azure portal, on the **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="85289-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="85289-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/zendesk-tutorial/tutorial_zendesk_samlbase.png)

1. <span data-ttu-id="85289-153">On the **Zendesk Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="85289-153">On the **Zendesk Domain and URLs** section, perform the following steps:</span></span>

    ![Zendesk Domain and URLs single sign-on information](./media/zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="85289-155">a.</span><span class="sxs-lookup"><span data-stu-id="85289-155">a.</span></span> <span data-ttu-id="85289-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="85289-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="85289-157">b.</span><span class="sxs-lookup"><span data-stu-id="85289-157">b.</span></span> <span data-ttu-id="85289-158">In the **Identifier** textbox, type the value using the following pattern: `<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="85289-158">In the **Identifier** textbox, type the value using the following pattern: `<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="85289-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="85289-159">These values are not real.</span></span> <span data-ttu-id="85289-160">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="85289-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="85289-161">Contact [Zendesk Client support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) to get these values.</span><span class="sxs-lookup"><span data-stu-id="85289-161">Contact [Zendesk Client support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) to get these values.</span></span>

1. <span data-ttu-id="85289-162">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span><span class="sxs-lookup"><span data-stu-id="85289-162">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![The Certificate download link](./media/zendesk-tutorial/tutorial_zendesk_certificate.png)

1. <span data-ttu-id="85289-164">Zendesk expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="85289-164">Zendesk expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="85289-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following the below steps:</span><span class="sxs-lookup"><span data-stu-id="85289-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following the below steps:</span></span> 

     ![Configure Single Sign-On](./media/zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="85289-167">a.</span><span class="sxs-lookup"><span data-stu-id="85289-167">a.</span></span> <span data-ttu-id="85289-168">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="85289-168">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On add](./media/zendesk-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On addattb](./media/zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="85289-171">b.</span><span class="sxs-lookup"><span data-stu-id="85289-171">b.</span></span> <span data-ttu-id="85289-172">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="85289-172">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="85289-173">c.</span><span class="sxs-lookup"><span data-stu-id="85289-173">c.</span></span> <span data-ttu-id="85289-174">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="85289-174">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="85289-175">d.</span><span class="sxs-lookup"><span data-stu-id="85289-175">d.</span></span> <span data-ttu-id="85289-176">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="85289-176">Click **Ok**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="85289-177">You use extension attributes to add attributes that are not in Azure AD by default.</span><span class="sxs-lookup"><span data-stu-id="85289-177">You use extension attributes to add attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="85289-178">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) to get the complete list of SAML attributes that **Zendesk** accepts.</span><span class="sxs-lookup"><span data-stu-id="85289-178">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) to get the complete list of SAML attributes that **Zendesk** accepts.</span></span>

1. <span data-ttu-id="85289-179">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="85289-179">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/zendesk-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="85289-181">On the **Zendesk Configuration** section, click **Configure Zendesk** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="85289-181">On the **Zendesk Configuration** section, click **Configure Zendesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="85289-182">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="85289-182">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Zendesk Configuration](./media/zendesk-tutorial/tutorial_zendesk_configure.png) 

1. <span data-ttu-id="85289-184">In a different web browser window, log into your Zendesk company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="85289-184">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

1. <span data-ttu-id="85289-185">Click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="85289-185">Click **Admin**.</span></span>

1. <span data-ttu-id="85289-186">In the left navigation pane, click **Settings**, and then click **Security**.</span><span class="sxs-lookup"><span data-stu-id="85289-186">In the left navigation pane, click **Settings**, and then click **Security**.</span></span>

1. <span data-ttu-id="85289-187">On the **Security** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="85289-187">On the **Security** page, perform the following steps:</span></span> 

     <span data-ttu-id="85289-188">![Security](./media/zendesk-tutorial/ic773089.png "Security")</span><span class="sxs-lookup"><span data-stu-id="85289-188">![Security](./media/zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="85289-189">![Single sign-on](./media/zendesk-tutorial/ic773090.png "Single sign-on")</span><span class="sxs-lookup"><span data-stu-id="85289-189">![Single sign-on](./media/zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="85289-190">a.</span><span class="sxs-lookup"><span data-stu-id="85289-190">a.</span></span> <span data-ttu-id="85289-191">Click the **Admin & Agents** tab.</span><span class="sxs-lookup"><span data-stu-id="85289-191">Click the **Admin & Agents** tab.</span></span>

     <span data-ttu-id="85289-192">b.</span><span class="sxs-lookup"><span data-stu-id="85289-192">b.</span></span> <span data-ttu-id="85289-193">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span><span class="sxs-lookup"><span data-stu-id="85289-193">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="85289-194">c.</span><span class="sxs-lookup"><span data-stu-id="85289-194">c.</span></span> <span data-ttu-id="85289-195">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="85289-195">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="85289-196">d.</span><span class="sxs-lookup"><span data-stu-id="85289-196">d.</span></span> <span data-ttu-id="85289-197">In **Remote Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="85289-197">In **Remote Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

     <span data-ttu-id="85289-198">e.</span><span class="sxs-lookup"><span data-stu-id="85289-198">e.</span></span> <span data-ttu-id="85289-199">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="85289-199">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>

     <span data-ttu-id="85289-200">f.</span><span class="sxs-lookup"><span data-stu-id="85289-200">f.</span></span> <span data-ttu-id="85289-201">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="85289-201">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="85289-202">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="85289-202">Create an Azure AD test user</span></span>

<span data-ttu-id="85289-203">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="85289-203">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="85289-205">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="85289-205">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="85289-206">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="85289-206">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/zendesk-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="85289-208">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="85289-208">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/zendesk-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="85289-210">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="85289-210">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/zendesk-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="85289-212">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="85289-212">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/zendesk-tutorial/create_aaduser_04.png)

    <span data-ttu-id="85289-214">a.</span><span class="sxs-lookup"><span data-stu-id="85289-214">a.</span></span> <span data-ttu-id="85289-215">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="85289-215">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="85289-216">b.</span><span class="sxs-lookup"><span data-stu-id="85289-216">b.</span></span> <span data-ttu-id="85289-217">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="85289-217">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="85289-218">c.</span><span class="sxs-lookup"><span data-stu-id="85289-218">c.</span></span> <span data-ttu-id="85289-219">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="85289-219">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="85289-220">d.</span><span class="sxs-lookup"><span data-stu-id="85289-220">d.</span></span> <span data-ttu-id="85289-221">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="85289-221">Click **Create**.</span></span>

### <a name="create-a-zendesk-test-user"></a><span data-ttu-id="85289-222">Create a Zendesk test user</span><span class="sxs-lookup"><span data-stu-id="85289-222">Create a Zendesk test user</span></span>

<span data-ttu-id="85289-223">The objective of this section is to create a user called Britta Simon in Zendesk.</span><span class="sxs-lookup"><span data-stu-id="85289-223">The objective of this section is to create a user called Britta Simon in Zendesk.</span></span> <span data-ttu-id="85289-224">Zendesk supports automatic user provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="85289-224">Zendesk supports automatic user provisioning, which is by default enabled.</span></span> <span data-ttu-id="85289-225">You can find more details [here](zendesk-provisioning-tutorial.md) on how to configure automatic user provisioning.</span><span class="sxs-lookup"><span data-stu-id="85289-225">You can find more details [here](zendesk-provisioning-tutorial.md) on how to configure automatic user provisioning.</span></span>

<span data-ttu-id="85289-226">**If you need to create user manually, please perform following steps:**</span><span class="sxs-lookup"><span data-stu-id="85289-226">**If you need to create user manually, please perform following steps:**</span></span>

> [!NOTE]
> <span data-ttu-id="85289-227">**End-user** accounts are automatically provisioned when signing in.</span><span class="sxs-lookup"><span data-stu-id="85289-227">**End-user** accounts are automatically provisioned when signing in.</span></span> <span data-ttu-id="85289-228">**Agent** and **Admin** accounts need to be manually provisioned in **Zendesk** before signing in.</span><span class="sxs-lookup"><span data-stu-id="85289-228">**Agent** and **Admin** accounts need to be manually provisioned in **Zendesk** before signing in.</span></span>

1. <span data-ttu-id="85289-229">Log in to your **Zendesk** tenant.</span><span class="sxs-lookup"><span data-stu-id="85289-229">Log in to your **Zendesk** tenant.</span></span>

1. <span data-ttu-id="85289-230">Select the **Customer List** tab.</span><span class="sxs-lookup"><span data-stu-id="85289-230">Select the **Customer List** tab.</span></span>

1. <span data-ttu-id="85289-231">Select the **User** tab, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="85289-231">Select the **User** tab, and click **Add**.</span></span>

    <span data-ttu-id="85289-232">![Add user](./media/zendesk-tutorial/ic773632.png "Add user")</span><span class="sxs-lookup"><span data-stu-id="85289-232">![Add user](./media/zendesk-tutorial/ic773632.png "Add user")</span></span>
1. <span data-ttu-id="85289-233">Type the **Name** and **Email** of an existing Azure AD account you want to provision, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="85289-233">Type the **Name** and **Email** of an existing Azure AD account you want to provision, and then click **Save**.</span></span>

    <span data-ttu-id="85289-234">![New user](./media/zendesk-tutorial/ic773633.png "New user")</span><span class="sxs-lookup"><span data-stu-id="85289-234">![New user](./media/zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="85289-235">You can use any other Zendesk user account creation tools or APIs provided by Zendesk to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="85289-235">You can use any other Zendesk user account creation tools or APIs provided by Zendesk to provision AAD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="85289-236">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="85289-236">Assign the Azure AD test user</span></span>

<span data-ttu-id="85289-237">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zendesk.</span><span class="sxs-lookup"><span data-stu-id="85289-237">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zendesk.</span></span>

![Assign the user role][200]

<span data-ttu-id="85289-239">**To assign Britta Simon to Zendesk, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="85289-239">**To assign Britta Simon to Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="85289-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="85289-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

1. <span data-ttu-id="85289-242">In the applications list, select **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="85289-242">In the applications list, select **Zendesk**.</span></span>

    ![The Zendesk link in the Applications list](./media/zendesk-tutorial/tutorial_zendesk_app.png)

1. <span data-ttu-id="85289-244">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="85289-244">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="85289-246">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="85289-246">Click **Add** button.</span></span> <span data-ttu-id="85289-247">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="85289-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="85289-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="85289-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="85289-250">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="85289-250">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="85289-251">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="85289-251">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="85289-252">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="85289-252">Test single sign-on</span></span>

<span data-ttu-id="85289-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="85289-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="85289-254">When you click the Zendesk tile in the Access Panel, you should get automatically signed-on to your Zendesk application.</span><span class="sxs-lookup"><span data-stu-id="85289-254">When you click the Zendesk tile in the Access Panel, you should get automatically signed-on to your Zendesk application.</span></span>
<span data-ttu-id="85289-255">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="85289-255">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="85289-256">Additional resources</span><span class="sxs-lookup"><span data-stu-id="85289-256">Additional resources</span></span>

* [<span data-ttu-id="85289-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="85289-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="85289-258">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="85289-258">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="85289-259">Configure User Provisioning</span><span class="sxs-lookup"><span data-stu-id="85289-259">Configure User Provisioning</span></span>](zendesk-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/zendesk-tutorial/tutorial_general_01.png
[2]: ./media/zendesk-tutorial/tutorial_general_02.png
[3]: ./media/zendesk-tutorial/tutorial_general_03.png
[4]: ./media/zendesk-tutorial/tutorial_general_04.png

[100]: ./media/zendesk-tutorial/tutorial_general_100.png

[200]: ./media/zendesk-tutorial/tutorial_general_200.png
[201]: ./media/zendesk-tutorial/tutorial_general_201.png
[202]: ./media/zendesk-tutorial/tutorial_general_202.png
[203]: ./media/zendesk-tutorial/tutorial_general_203.png
