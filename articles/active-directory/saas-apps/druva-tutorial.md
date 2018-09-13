---
title: 'Tutorial: Azure Active Directory integration with Druva | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Druva.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2017
ms.author: jeedes
ms.openlocfilehash: 985304244acdfafa4fa99dbbe876f35b3e6c58b2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871219"
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a><span data-ttu-id="6e489-103">Tutorial: Azure Active Directory integration with Druva</span><span class="sxs-lookup"><span data-stu-id="6e489-103">Tutorial: Azure Active Directory integration with Druva</span></span>

<span data-ttu-id="6e489-104">In this tutorial, you learn how to integrate Druva with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6e489-104">In this tutorial, you learn how to integrate Druva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6e489-105">Integrating Druva with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="6e489-105">Integrating Druva with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6e489-106">You can control in Azure AD who has access to Druva.</span><span class="sxs-lookup"><span data-stu-id="6e489-106">You can control in Azure AD who has access to Druva.</span></span>
- <span data-ttu-id="6e489-107">You can enable your users to automatically get signed-on to Druva (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="6e489-107">You can enable your users to automatically get signed-on to Druva (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6e489-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6e489-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="6e489-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="6e489-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e489-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6e489-110">Prerequisites</span></span>

<span data-ttu-id="6e489-111">To configure Azure AD integration with Druva, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="6e489-111">To configure Azure AD integration with Druva, you need the following items:</span></span>

- <span data-ttu-id="6e489-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="6e489-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6e489-113">A Druva single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="6e489-113">A Druva single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6e489-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="6e489-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6e489-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="6e489-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6e489-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="6e489-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6e489-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6e489-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6e489-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="6e489-118">Scenario description</span></span>
<span data-ttu-id="6e489-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="6e489-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6e489-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="6e489-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6e489-121">Adding Druva from the gallery</span><span class="sxs-lookup"><span data-stu-id="6e489-121">Adding Druva from the gallery</span></span>
1. <span data-ttu-id="6e489-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6e489-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-druva-from-the-gallery"></a><span data-ttu-id="6e489-123">Adding Druva from the gallery</span><span class="sxs-lookup"><span data-stu-id="6e489-123">Adding Druva from the gallery</span></span>
<span data-ttu-id="6e489-124">To configure the integration of Druva into Azure AD, you need to add Druva from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="6e489-124">To configure the integration of Druva into Azure AD, you need to add Druva from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6e489-125">**To add Druva from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6e489-125">**To add Druva from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6e489-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="6e489-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="6e489-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="6e489-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6e489-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6e489-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="6e489-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="6e489-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="6e489-133">In the search box, type **Druva**, select **Druva** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="6e489-133">In the search box, type **Druva**, select **Druva** from result panel then click **Add** button to add the application.</span></span>

    ![Druva in the results list](./media/druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6e489-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6e489-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6e489-136">In this section, you configure and test Azure AD single sign-on with Druva based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6e489-136">In this section, you configure and test Azure AD single sign-on with Druva based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6e489-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Druva is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e489-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Druva is to a user in Azure AD.</span></span> <span data-ttu-id="6e489-138">In other words, a link relationship between an Azure AD user and the related user in Druva needs to be established.</span><span class="sxs-lookup"><span data-stu-id="6e489-138">In other words, a link relationship between an Azure AD user and the related user in Druva needs to be established.</span></span>

<span data-ttu-id="6e489-139">In Druva, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="6e489-139">In Druva, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6e489-140">To configure and test Azure AD single sign-on with Druva, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6e489-140">To configure and test Azure AD single sign-on with Druva, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6e489-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="6e489-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="6e489-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6e489-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="6e489-143">**[Create a Druva test user](#create-a-druva-test-user)** - to have a counterpart of Britta Simon in Druva that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="6e489-143">**[Create a Druva test user](#create-a-druva-test-user)** - to have a counterpart of Britta Simon in Druva that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="6e489-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6e489-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="6e489-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="6e489-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6e489-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6e489-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6e489-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Druva application.</span><span class="sxs-lookup"><span data-stu-id="6e489-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Druva application.</span></span>

<span data-ttu-id="6e489-148">**To configure Azure AD single sign-on with Druva, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6e489-148">**To configure Azure AD single sign-on with Druva, perform the following steps:**</span></span>

1. <span data-ttu-id="6e489-149">In the Azure portal, on the **Druva** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6e489-149">In the Azure portal, on the **Druva** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="6e489-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6e489-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/druva-tutorial/tutorial_druva_samlbase.png)

1. <span data-ttu-id="6e489-153">On the **Druva Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="6e489-153">On the **Druva Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/druva-tutorial/tutorial_druva_url.png)

    <span data-ttu-id="6e489-155">In the **Identifier** textbox, type the string value: `druva-cloud`</span><span class="sxs-lookup"><span data-stu-id="6e489-155">In the **Identifier** textbox, type the string value: `druva-cloud`</span></span>
    
1. <span data-ttu-id="6e489-156">Check **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="6e489-156">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="6e489-157">If you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="6e489-157">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/druva-tutorial/tutorial_druva_url1.png)
    
    <span data-ttu-id="6e489-159">In the **Sign-on URL** textbox, type the URL: `https://cloud.druva.com/home`</span><span class="sxs-lookup"><span data-stu-id="6e489-159">In the **Sign-on URL** textbox, type the URL: `https://cloud.druva.com/home`</span></span>

1. <span data-ttu-id="6e489-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="6e489-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/druva-tutorial/tutorial_druva_certificate.png) 

1. <span data-ttu-id="6e489-162">Your Druva application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span><span class="sxs-lookup"><span data-stu-id="6e489-162">Your Druva application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span> 

    ![Configure Single Sign-On](./media/druva-tutorial/tutorial_druva_attribute.png)

1. <span data-ttu-id="6e489-164">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6e489-164">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>

    | <span data-ttu-id="6e489-165">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="6e489-165">Attribute Name</span></span>      | <span data-ttu-id="6e489-166">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="6e489-166">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="6e489-167">insync\_auth\_token</span><span class="sxs-lookup"><span data-stu-id="6e489-167">insync\_auth\_token</span></span> |<span data-ttu-id="6e489-168">Enter the token generated value</span><span class="sxs-lookup"><span data-stu-id="6e489-168">Enter the token generated value</span></span> |
    
    <span data-ttu-id="6e489-169">a.</span><span class="sxs-lookup"><span data-stu-id="6e489-169">a.</span></span> <span data-ttu-id="6e489-170">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="6e489-170">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
    
    ![Configure Single Sign-On](./media/druva-tutorial/tutorial_attribute_04.png)
    
    ![Configure Single Sign-On](./media/druva-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="6e489-173">b.</span><span class="sxs-lookup"><span data-stu-id="6e489-173">b.</span></span> <span data-ttu-id="6e489-174">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="6e489-174">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="6e489-175">c.</span><span class="sxs-lookup"><span data-stu-id="6e489-175">c.</span></span> <span data-ttu-id="6e489-176">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="6e489-176">From the **Value** list, type the attribute value shown for that row.</span></span> <span data-ttu-id="6e489-177">The token generated value is explained later in tutorial.</span><span class="sxs-lookup"><span data-stu-id="6e489-177">The token generated value is explained later in tutorial.</span></span>
    
    <span data-ttu-id="6e489-178">d.</span><span class="sxs-lookup"><span data-stu-id="6e489-178">d.</span></span> <span data-ttu-id="6e489-179">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="6e489-179">Click **Ok**.</span></span>    

1. <span data-ttu-id="6e489-180">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="6e489-180">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/druva-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="6e489-182">On the **Druva Configuration** section, click **Configure Druva** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="6e489-182">On the **Druva Configuration** section, click **Configure Druva** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6e489-183">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="6e489-183">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/druva-tutorial/tutorial_druva_configure.png) 

1. <span data-ttu-id="6e489-185">In a different web browser window, log in to your Druva company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="6e489-185">In a different web browser window, log in to your Druva company site as an administrator.</span></span>

1. <span data-ttu-id="6e489-186">Go to **Manage \> Settings**.</span><span class="sxs-lookup"><span data-stu-id="6e489-186">Go to **Manage \> Settings**.</span></span>

    <span data-ttu-id="6e489-187">![Settings](./media/druva-tutorial/ic795091.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="6e489-187">![Settings](./media/druva-tutorial/ic795091.png "Settings")</span></span>

1. <span data-ttu-id="6e489-188">On the Single Sign-On Settings dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6e489-188">On the Single Sign-On Settings dialog, perform the following steps:</span></span>

    <span data-ttu-id="6e489-189">![Single Sign-On Settings](./media/druva-tutorial/ic795092.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="6e489-189">![Single Sign-On Settings](./media/druva-tutorial/ic795092.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="6e489-190">a.</span><span class="sxs-lookup"><span data-stu-id="6e489-190">a.</span></span> <span data-ttu-id="6e489-191">In **ID Provider Login URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6e489-191">In **ID Provider Login URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
        
    <span data-ttu-id="6e489-192">b.</span><span class="sxs-lookup"><span data-stu-id="6e489-192">b.</span></span> <span data-ttu-id="6e489-193">In **ID Provider Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal</span><span class="sxs-lookup"><span data-stu-id="6e489-193">In **ID Provider Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal</span></span>
        
    <span data-ttu-id="6e489-194">c.</span><span class="sxs-lookup"><span data-stu-id="6e489-194">c.</span></span> <span data-ttu-id="6e489-195">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **ID Provider Certificate** textbox</span><span class="sxs-lookup"><span data-stu-id="6e489-195">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **ID Provider Certificate** textbox</span></span>
     
    <span data-ttu-id="6e489-196">d.</span><span class="sxs-lookup"><span data-stu-id="6e489-196">d.</span></span> <span data-ttu-id="6e489-197">To open the **Settings** page, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="6e489-197">To open the **Settings** page, click **Save**.</span></span>

1. <span data-ttu-id="6e489-198">On the **Settings** page, click **Generate SSO Token**.</span><span class="sxs-lookup"><span data-stu-id="6e489-198">On the **Settings** page, click **Generate SSO Token**.</span></span>

    <span data-ttu-id="6e489-199">![Settings](./media/druva-tutorial/ic795093.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="6e489-199">![Settings](./media/druva-tutorial/ic795093.png "Settings")</span></span>

1. <span data-ttu-id="6e489-200">On the **Single Sign-on Authentication Token** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6e489-200">On the **Single Sign-on Authentication Token** dialog, perform the following steps:</span></span>

    <span data-ttu-id="6e489-201">![SSO Token](./media/druva-tutorial/ic795094.png "SSO Token")</span><span class="sxs-lookup"><span data-stu-id="6e489-201">![SSO Token](./media/druva-tutorial/ic795094.png "SSO Token")</span></span>
    
    <span data-ttu-id="6e489-202">a.</span><span class="sxs-lookup"><span data-stu-id="6e489-202">a.</span></span> <span data-ttu-id="6e489-203">Click **Copy**, Paste copied value in the **Value** textbox in the **Add Attribute** section in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6e489-203">Click **Copy**, Paste copied value in the **Value** textbox in the **Add Attribute** section in the Azure portal.</span></span>
    
    <span data-ttu-id="6e489-204">b.</span><span class="sxs-lookup"><span data-stu-id="6e489-204">b.</span></span> <span data-ttu-id="6e489-205">Click **Close**.</span><span class="sxs-lookup"><span data-stu-id="6e489-205">Click **Close**.</span></span>

> [!TIP]
> <span data-ttu-id="6e489-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="6e489-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6e489-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="6e489-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6e489-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6e489-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6e489-209">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6e489-209">Create an Azure AD test user</span></span>

<span data-ttu-id="6e489-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6e489-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="6e489-212">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6e489-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6e489-213">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="6e489-213">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/druva-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="6e489-215">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="6e489-215">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/druva-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="6e489-217">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="6e489-217">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/druva-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="6e489-219">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6e489-219">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/druva-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6e489-221">a.</span><span class="sxs-lookup"><span data-stu-id="6e489-221">a.</span></span> <span data-ttu-id="6e489-222">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6e489-222">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6e489-223">b.</span><span class="sxs-lookup"><span data-stu-id="6e489-223">b.</span></span> <span data-ttu-id="6e489-224">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6e489-224">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="6e489-225">c.</span><span class="sxs-lookup"><span data-stu-id="6e489-225">c.</span></span> <span data-ttu-id="6e489-226">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="6e489-226">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="6e489-227">d.</span><span class="sxs-lookup"><span data-stu-id="6e489-227">d.</span></span> <span data-ttu-id="6e489-228">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6e489-228">Click **Create**.</span></span>
 
### <a name="create-a-druva-test-user"></a><span data-ttu-id="6e489-229">Create a Druva test user</span><span class="sxs-lookup"><span data-stu-id="6e489-229">Create a Druva test user</span></span>

<span data-ttu-id="6e489-230">In order to enable Azure AD users to log in to Druva, they must be provisioned into Druva.</span><span class="sxs-lookup"><span data-stu-id="6e489-230">In order to enable Azure AD users to log in to Druva, they must be provisioned into Druva.</span></span> <span data-ttu-id="6e489-231">In the case of Druva, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="6e489-231">In the case of Druva, provisioning is a manual task.</span></span>

<span data-ttu-id="6e489-232">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6e489-232">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="6e489-233">Log in to your **Druva** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="6e489-233">Log in to your **Druva** company site as administrator.</span></span>

1. <span data-ttu-id="6e489-234">Go to **Manage \> Users**.</span><span class="sxs-lookup"><span data-stu-id="6e489-234">Go to **Manage \> Users**.</span></span>
   
   <span data-ttu-id="6e489-235">![Manage Users](./media/druva-tutorial/ic795097.png "Manage Users")</span><span class="sxs-lookup"><span data-stu-id="6e489-235">![Manage Users](./media/druva-tutorial/ic795097.png "Manage Users")</span></span>

1. <span data-ttu-id="6e489-236">Click **Create New**.</span><span class="sxs-lookup"><span data-stu-id="6e489-236">Click **Create New**.</span></span>
   
   <span data-ttu-id="6e489-237">![Manage Users](./media/druva-tutorial/ic795098.png "Manage Users")</span><span class="sxs-lookup"><span data-stu-id="6e489-237">![Manage Users](./media/druva-tutorial/ic795098.png "Manage Users")</span></span>

1. <span data-ttu-id="6e489-238">On the Create New User dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6e489-238">On the Create New User dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="6e489-239">![Create NewUser](./media/druva-tutorial/ic795099.png "Create NewUser")</span><span class="sxs-lookup"><span data-stu-id="6e489-239">![Create NewUser](./media/druva-tutorial/ic795099.png "Create NewUser")</span></span>
   
   <span data-ttu-id="6e489-240">a.</span><span class="sxs-lookup"><span data-stu-id="6e489-240">a.</span></span> <span data-ttu-id="6e489-241">In the **Email address** textbox, enter the email of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="6e489-241">In the **Email address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="6e489-242">b.</span><span class="sxs-lookup"><span data-stu-id="6e489-242">b.</span></span> <span data-ttu-id="6e489-243">In the **Name** textbox, enter the name of user like **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6e489-243">In the **Name** textbox, enter the name of user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="6e489-244">c.</span><span class="sxs-lookup"><span data-stu-id="6e489-244">c.</span></span> <span data-ttu-id="6e489-245">Click **Create User**.</span><span class="sxs-lookup"><span data-stu-id="6e489-245">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="6e489-246">You can use any other Druva user account creation tools or APIs provided by Druva to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="6e489-246">You can use any other Druva user account creation tools or APIs provided by Druva to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6e489-247">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6e489-247">Assign the Azure AD test user</span></span>

<span data-ttu-id="6e489-248">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Druva.</span><span class="sxs-lookup"><span data-stu-id="6e489-248">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Druva.</span></span>

![Assign the user role][200] 

<span data-ttu-id="6e489-250">**To assign Britta Simon to Druva, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6e489-250">**To assign Britta Simon to Druva, perform the following steps:**</span></span>

1. <span data-ttu-id="6e489-251">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6e489-251">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="6e489-253">In the applications list, select **Druva**.</span><span class="sxs-lookup"><span data-stu-id="6e489-253">In the applications list, select **Druva**.</span></span>

    ![The Druva link in the Applications list](./media/druva-tutorial/tutorial_druva_app.png)  

1. <span data-ttu-id="6e489-255">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="6e489-255">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="6e489-257">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="6e489-257">Click **Add** button.</span></span> <span data-ttu-id="6e489-258">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6e489-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="6e489-260">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="6e489-260">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="6e489-261">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="6e489-261">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="6e489-262">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6e489-262">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6e489-263">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="6e489-263">Test single sign-on</span></span>

<span data-ttu-id="6e489-264">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="6e489-264">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6e489-265">When you click the Druva tile in the Access Panel, you should get automatically signed-on to your Druva application.</span><span class="sxs-lookup"><span data-stu-id="6e489-265">When you click the Druva tile in the Access Panel, you should get automatically signed-on to your Druva application.</span></span>
<span data-ttu-id="6e489-266">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6e489-266">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6e489-267">Additional resources</span><span class="sxs-lookup"><span data-stu-id="6e489-267">Additional resources</span></span>

* [<span data-ttu-id="6e489-268">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6e489-268">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="6e489-269">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6e489-269">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/druva-tutorial/tutorial_general_01.png
[2]: ./media/druva-tutorial/tutorial_general_02.png
[3]: ./media/druva-tutorial/tutorial_general_03.png
[4]: ./media/druva-tutorial/tutorial_general_04.png

[100]: ./media/druva-tutorial/tutorial_general_100.png

[200]: ./media/druva-tutorial/tutorial_general_200.png
[201]: ./media/druva-tutorial/tutorial_general_201.png
[202]: ./media/druva-tutorial/tutorial_general_202.png
[203]: ./media/druva-tutorial/tutorial_general_203.png

