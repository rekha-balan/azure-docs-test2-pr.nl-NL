---
title: 'Tutorial: Azure Active Directory integration with TimeOffManager | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and TimeOffManager.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: e7f0f6bb778dedeea61b74b5ca0c2edbadd5279b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869759"
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a><span data-ttu-id="cade7-103">Tutorial: Azure Active Directory integration with TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="cade7-103">Tutorial: Azure Active Directory integration with TimeOffManager</span></span>

<span data-ttu-id="cade7-104">In this tutorial, you learn how to integrate TimeOffManager with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cade7-104">In this tutorial, you learn how to integrate TimeOffManager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cade7-105">Integrating TimeOffManager with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="cade7-105">Integrating TimeOffManager with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cade7-106">You can control in Azure AD who has access to TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="cade7-106">You can control in Azure AD who has access to TimeOffManager</span></span>
- <span data-ttu-id="cade7-107">You can enable your users to automatically get signed-on to TimeOffManager (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="cade7-107">You can enable your users to automatically get signed-on to TimeOffManager (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cade7-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="cade7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cade7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="cade7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cade7-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cade7-110">Prerequisites</span></span>

<span data-ttu-id="cade7-111">To configure Azure AD integration with TimeOffManager, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="cade7-111">To configure Azure AD integration with TimeOffManager, you need the following items:</span></span>

- <span data-ttu-id="cade7-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="cade7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cade7-113">A TimeOffManager single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="cade7-113">A TimeOffManager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cade7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="cade7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cade7-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="cade7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cade7-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="cade7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cade7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cade7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cade7-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="cade7-118">Scenario description</span></span>
<span data-ttu-id="cade7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="cade7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cade7-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="cade7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cade7-121">Add TimeOffManager from the gallery</span><span class="sxs-lookup"><span data-stu-id="cade7-121">Add TimeOffManager from the gallery</span></span>
1. <span data-ttu-id="cade7-122">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cade7-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-timeoffmanager-from-the-gallery"></a><span data-ttu-id="cade7-123">Add TimeOffManager from the gallery</span><span class="sxs-lookup"><span data-stu-id="cade7-123">Add TimeOffManager from the gallery</span></span>
<span data-ttu-id="cade7-124">To configure the integration of TimeOffManager into Azure AD, you need to add TimeOffManager from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="cade7-124">To configure the integration of TimeOffManager into Azure AD, you need to add TimeOffManager from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cade7-125">**To add TimeOffManager from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cade7-125">**To add TimeOffManager from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cade7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="cade7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="cade7-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="cade7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cade7-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cade7-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="cade7-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="cade7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="cade7-133">In the search box, type **TimeOffManager**, select **TimeOffManager** from result panel and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="cade7-133">In the search box, type **TimeOffManager**, select **TimeOffManager** from result panel and then click **Add** button to add the application.</span></span>

    ![Add from gallery](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="cade7-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cade7-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="cade7-136">In this section, you configure and test Azure AD single sign-on with TimeOffManager based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cade7-136">In this section, you configure and test Azure AD single sign-on with TimeOffManager based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cade7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TimeOffManager is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cade7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TimeOffManager is to a user in Azure AD.</span></span> <span data-ttu-id="cade7-138">In other words, a link relationship between an Azure AD user and the related user in TimeOffManager needs to be established.</span><span class="sxs-lookup"><span data-stu-id="cade7-138">In other words, a link relationship between an Azure AD user and the related user in TimeOffManager needs to be established.</span></span>

<span data-ttu-id="cade7-139">In TimeOffManager, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="cade7-139">In TimeOffManager, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cade7-140">To configure and test Azure AD single sign-on with TimeOffManager, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="cade7-140">To configure and test Azure AD single sign-on with TimeOffManager, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cade7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="cade7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="cade7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cade7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="cade7-143">**[Create a TimeOffManager test user](#create-a-timeoffmanager-test-user)** - to have a counterpart of Britta Simon in TimeOffManager that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="cade7-143">**[Create a TimeOffManager test user](#create-a-timeoffmanager-test-user)** - to have a counterpart of Britta Simon in TimeOffManager that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="cade7-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cade7-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="cade7-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="cade7-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="cade7-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cade7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="cade7-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TimeOffManager application.</span><span class="sxs-lookup"><span data-stu-id="cade7-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TimeOffManager application.</span></span>

<span data-ttu-id="cade7-148">**To configure Azure AD single sign-on with TimeOffManager, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cade7-148">**To configure Azure AD single sign-on with TimeOffManager, perform the following steps:**</span></span>

1. <span data-ttu-id="cade7-149">In the Azure portal, on the **TimeOffManager** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="cade7-149">In the Azure portal, on the **TimeOffManager** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="cade7-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cade7-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML based Sign-On](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

1. <span data-ttu-id="cade7-153">On the **TimeOffManager Domain and URLs** section, perform the following:</span><span class="sxs-lookup"><span data-stu-id="cade7-153">On the **TimeOffManager Domain and URLs** section, perform the following:</span></span>

     ![TimeOffManager Domain and URLs section](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    <span data-ttu-id="cade7-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span><span class="sxs-lookup"><span data-stu-id="cade7-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cade7-156">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="cade7-156">This value is not real.</span></span> <span data-ttu-id="cade7-157">Update this value with the actual Reply URL.</span><span class="sxs-lookup"><span data-stu-id="cade7-157">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="cade7-158">You can get this value from **Single Sign on settings page** which is explained later in the tutorial or Contact [TimeOffManager support team](https://www.purelyhr.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="cade7-158">You can get this value from **Single Sign on settings page** which is explained later in the tutorial or Contact [TimeOffManager support team](https://www.purelyhr.com/contact-us).</span></span>
 
1. <span data-ttu-id="cade7-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="cade7-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![SAML Signing Certificate section](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

1. <span data-ttu-id="cade7-161">The objective of this section is to outline how to enable users to authenticate to TimeOffManger with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="cade7-161">The objective of this section is to outline how to enable users to authenticate to TimeOffManger with their account in Azure AD using federation based on the SAML protocol.</span></span>
    
    <span data-ttu-id="cade7-162">Your TimeOffManger application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="cade7-162">Your TimeOffManger application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="cade7-163">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="cade7-163">The following screenshot shows an example for this.</span></span>

    <span data-ttu-id="cade7-164">![saml token attributes](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span><span class="sxs-lookup"><span data-stu-id="cade7-164">![saml token attributes](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span></span>
    
    | <span data-ttu-id="cade7-165">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="cade7-165">Attribute Name</span></span> | <span data-ttu-id="cade7-166">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="cade7-166">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="cade7-167">Firstname</span><span class="sxs-lookup"><span data-stu-id="cade7-167">Firstname</span></span> |<span data-ttu-id="cade7-168">User.givenname</span><span class="sxs-lookup"><span data-stu-id="cade7-168">User.givenname</span></span> |
    | <span data-ttu-id="cade7-169">Lastname</span><span class="sxs-lookup"><span data-stu-id="cade7-169">Lastname</span></span> |<span data-ttu-id="cade7-170">User.surname</span><span class="sxs-lookup"><span data-stu-id="cade7-170">User.surname</span></span> |
    | <span data-ttu-id="cade7-171">Email</span><span class="sxs-lookup"><span data-stu-id="cade7-171">Email</span></span> |<span data-ttu-id="cade7-172">User.mail</span><span class="sxs-lookup"><span data-stu-id="cade7-172">User.mail</span></span> |
    
    <span data-ttu-id="cade7-173">a.</span><span class="sxs-lookup"><span data-stu-id="cade7-173">a.</span></span>  <span data-ttu-id="cade7-174">For each data row in the table above, click **add user attribute**.</span><span class="sxs-lookup"><span data-stu-id="cade7-174">For each data row in the table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="cade7-175">![saml token attributes](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span><span class="sxs-lookup"><span data-stu-id="cade7-175">![saml token attributes](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span></span>
    
    <span data-ttu-id="cade7-176">![saml token attributes](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span><span class="sxs-lookup"><span data-stu-id="cade7-176">![saml token attributes](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span></span>
    
    <span data-ttu-id="cade7-177">b.</span><span class="sxs-lookup"><span data-stu-id="cade7-177">b.</span></span>  <span data-ttu-id="cade7-178">In the **Attribute Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="cade7-178">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="cade7-179">c.</span><span class="sxs-lookup"><span data-stu-id="cade7-179">c.</span></span>  <span data-ttu-id="cade7-180">In the **Attribute Value** textbox, select the attribute  value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="cade7-180">In the **Attribute Value** textbox, select the attribute  value shown for that row.</span></span>
    
    <span data-ttu-id="cade7-181">d.</span><span class="sxs-lookup"><span data-stu-id="cade7-181">d.</span></span>  <span data-ttu-id="cade7-182">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="cade7-182">Click **Ok**.</span></span>
    
1. <span data-ttu-id="cade7-183">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="cade7-183">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/timeoffmanager-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="cade7-185">On the **TimeOffManager Configuration** section, click **Configure TimeOffManager** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="cade7-185">On the **TimeOffManager Configuration** section, click **Configure TimeOffManager** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cade7-186">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="cade7-186">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![TimeOffManager Configuration section](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

1. <span data-ttu-id="cade7-188">In a different web browser window, log into your TimeOffManager company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="cade7-188">In a different web browser window, log into your TimeOffManager company site as an administrator.</span></span>

1. <span data-ttu-id="cade7-189">Go to **Account \> Account Options \> Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="cade7-189">Go to **Account \> Account Options \> Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="cade7-190">![Single Sign-On Settings](./media/timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="cade7-190">![Single Sign-On Settings](./media/timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span></span>
1. <span data-ttu-id="cade7-191">In the **Single Sign-On Settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cade7-191">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="cade7-192">![Single Sign-On Settings](./media/timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="cade7-192">![Single Sign-On Settings](./media/timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="cade7-193">a.</span><span class="sxs-lookup"><span data-stu-id="cade7-193">a.</span></span> <span data-ttu-id="cade7-194">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="cade7-194">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>
   
   <span data-ttu-id="cade7-195">b.</span><span class="sxs-lookup"><span data-stu-id="cade7-195">b.</span></span> <span data-ttu-id="cade7-196">In **Idp Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cade7-196">In **Idp Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="cade7-197">c.</span><span class="sxs-lookup"><span data-stu-id="cade7-197">c.</span></span> <span data-ttu-id="cade7-198">In **IdP Endpoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cade7-198">In **IdP Endpoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="cade7-199">d.</span><span class="sxs-lookup"><span data-stu-id="cade7-199">d.</span></span> <span data-ttu-id="cade7-200">As **Enforce SAML**, select **No**.</span><span class="sxs-lookup"><span data-stu-id="cade7-200">As **Enforce SAML**, select **No**.</span></span>
   
   <span data-ttu-id="cade7-201">e.</span><span class="sxs-lookup"><span data-stu-id="cade7-201">e.</span></span> <span data-ttu-id="cade7-202">As **Auto-Create Users**, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="cade7-202">As **Auto-Create Users**, select **Yes**.</span></span>
   
   <span data-ttu-id="cade7-203">f.</span><span class="sxs-lookup"><span data-stu-id="cade7-203">f.</span></span> <span data-ttu-id="cade7-204">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cade7-204">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="cade7-205">g.</span><span class="sxs-lookup"><span data-stu-id="cade7-205">g.</span></span> <span data-ttu-id="cade7-206">click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="cade7-206">click **Save Changes**.</span></span>

1. <span data-ttu-id="cade7-207">In **Single Sign on settings** page, copy the value of **Assertion Consumer Service URL** and paste it in the **Reply URL** text box under **TimeOffManager Domain and URLs** section in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cade7-207">In **Single Sign on settings** page, copy the value of **Assertion Consumer Service URL** and paste it in the **Reply URL** text box under **TimeOffManager Domain and URLs** section in Azure portal.</span></span> 

      <span data-ttu-id="cade7-208">![Single Sign-On Settings](./media/timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="cade7-208">![Single Sign-On Settings](./media/timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span></span>

> [!TIP]
> <span data-ttu-id="cade7-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="cade7-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cade7-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="cade7-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cade7-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cade7-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="cade7-212">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cade7-212">Create an Azure AD test user</span></span>
<span data-ttu-id="cade7-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cade7-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="cade7-215">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cade7-215">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cade7-216">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="cade7-216">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/timeoffmanager-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="cade7-218">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="cade7-218">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Users and groups --> All users](./media/timeoffmanager-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="cade7-220">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="cade7-220">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Add Button](./media/timeoffmanager-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="cade7-222">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cade7-222">On the **User** dialog page, perform the following steps:</span></span>
 
    ![User dialog page](./media/timeoffmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cade7-224">a.</span><span class="sxs-lookup"><span data-stu-id="cade7-224">a.</span></span> <span data-ttu-id="cade7-225">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cade7-225">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cade7-226">b.</span><span class="sxs-lookup"><span data-stu-id="cade7-226">b.</span></span> <span data-ttu-id="cade7-227">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cade7-227">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cade7-228">c.</span><span class="sxs-lookup"><span data-stu-id="cade7-228">c.</span></span> <span data-ttu-id="cade7-229">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="cade7-229">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cade7-230">d.</span><span class="sxs-lookup"><span data-stu-id="cade7-230">d.</span></span> <span data-ttu-id="cade7-231">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="cade7-231">Click **Create**.</span></span>
 
### <a name="create-a-timeoffmanager-test-user"></a><span data-ttu-id="cade7-232">Create a TimeOffManager test user</span><span class="sxs-lookup"><span data-stu-id="cade7-232">Create a TimeOffManager test user</span></span>

<span data-ttu-id="cade7-233">In order to enable Azure AD users to log into TimeOffManager, they must be provisioned to TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="cade7-233">In order to enable Azure AD users to log into TimeOffManager, they must be provisioned to TimeOffManager.</span></span>  

<span data-ttu-id="cade7-234">TimeOffManager supports just in time user provisioning.</span><span class="sxs-lookup"><span data-stu-id="cade7-234">TimeOffManager supports just in time user provisioning.</span></span> <span data-ttu-id="cade7-235">There is no action item for you.</span><span class="sxs-lookup"><span data-stu-id="cade7-235">There is no action item for you.</span></span>  

<span data-ttu-id="cade7-236">The users are added automatically during the first login using single sign on.</span><span class="sxs-lookup"><span data-stu-id="cade7-236">The users are added automatically during the first login using single sign on.</span></span>

>[!NOTE]
><span data-ttu-id="cade7-237">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="cade7-237">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager to provision Azure AD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="cade7-238">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cade7-238">Assign the Azure AD test user</span></span>

<span data-ttu-id="cade7-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="cade7-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TimeOffManager.</span></span>

![Assign User][200] 

<span data-ttu-id="cade7-241">**To assign Britta Simon to TimeOffManager, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cade7-241">**To assign Britta Simon to TimeOffManager, perform the following steps:**</span></span>

1. <span data-ttu-id="cade7-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cade7-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="cade7-244">In the applications list, select **TimeOffManager**.</span><span class="sxs-lookup"><span data-stu-id="cade7-244">In the applications list, select **TimeOffManager**.</span></span>

    ![TimeOffManager in app list](./media/timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

1. <span data-ttu-id="cade7-246">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="cade7-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="cade7-248">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="cade7-248">Click **Add** button.</span></span> <span data-ttu-id="cade7-249">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="cade7-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="cade7-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="cade7-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="cade7-252">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="cade7-252">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="cade7-253">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="cade7-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="cade7-254">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="cade7-254">Test single sign-on</span></span>

<span data-ttu-id="cade7-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="cade7-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cade7-256">When you click the TimeOffManager tile in the Access Panel, you should get automatically signed-on to your TimeOffManager application.</span><span class="sxs-lookup"><span data-stu-id="cade7-256">When you click the TimeOffManager tile in the Access Panel, you should get automatically signed-on to your TimeOffManager application.</span></span> <span data-ttu-id="cade7-257">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cade7-257">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cade7-258">Additional resources</span><span class="sxs-lookup"><span data-stu-id="cade7-258">Additional resources</span></span>

* [<span data-ttu-id="cade7-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cade7-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="cade7-260">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cade7-260">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/timeoffmanager-tutorial/tutorial_general_203.png

