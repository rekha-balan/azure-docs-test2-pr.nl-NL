---
title: 'Tutorial: Azure Active Directory integration with Dome9 Arc | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Dome9 Arc.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4c12875f-de71-40cb-b9ac-216a805334e5
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2018
ms.author: jeedes
ms.openlocfilehash: 934520764749b5abce9aefe22b8eb9a5d8e490f2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858039"
---
# <a name="tutorial-azure-active-directory-integration-with-dome9-arc"></a><span data-ttu-id="02adc-103">Tutorial: Azure Active Directory integration with Dome9 Arc</span><span class="sxs-lookup"><span data-stu-id="02adc-103">Tutorial: Azure Active Directory integration with Dome9 Arc</span></span>

<span data-ttu-id="02adc-104">In this tutorial, you learn how to integrate Dome9 Arc with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="02adc-104">In this tutorial, you learn how to integrate Dome9 Arc with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="02adc-105">Integrating Dome9 Arc with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="02adc-105">Integrating Dome9 Arc with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="02adc-106">You can control in Azure AD who has access to Dome9 Arc.</span><span class="sxs-lookup"><span data-stu-id="02adc-106">You can control in Azure AD who has access to Dome9 Arc.</span></span>
- <span data-ttu-id="02adc-107">You can enable your users to automatically get signed-on to Dome9 Arc (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="02adc-107">You can enable your users to automatically get signed-on to Dome9 Arc (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="02adc-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="02adc-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="02adc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="02adc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02adc-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="02adc-110">Prerequisites</span></span>

<span data-ttu-id="02adc-111">To configure Azure AD integration with Dome9 Arc, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="02adc-111">To configure Azure AD integration with Dome9 Arc, you need the following items:</span></span>

- <span data-ttu-id="02adc-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="02adc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="02adc-113">A Dome9 Arc single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="02adc-113">A Dome9 Arc single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="02adc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="02adc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="02adc-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="02adc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="02adc-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="02adc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="02adc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="02adc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="02adc-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="02adc-118">Scenario description</span></span>

<span data-ttu-id="02adc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="02adc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="02adc-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="02adc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="02adc-121">Adding Dome9 Arc from the gallery</span><span class="sxs-lookup"><span data-stu-id="02adc-121">Adding Dome9 Arc from the gallery</span></span>
2. <span data-ttu-id="02adc-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="02adc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dome9-arc-from-the-gallery"></a><span data-ttu-id="02adc-123">Adding Dome9 Arc from the gallery</span><span class="sxs-lookup"><span data-stu-id="02adc-123">Adding Dome9 Arc from the gallery</span></span>

<span data-ttu-id="02adc-124">To configure the integration of Dome9 Arc into Azure AD, you need to add Dome9 Arc from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="02adc-124">To configure the integration of Dome9 Arc into Azure AD, you need to add Dome9 Arc from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="02adc-125">**To add Dome9 Arc from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="02adc-125">**To add Dome9 Arc from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="02adc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="02adc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="02adc-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="02adc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="02adc-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="02adc-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="02adc-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="02adc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="02adc-133">In the search box, type **Dome9 Arc**, select **Dome9 Arc** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="02adc-133">In the search box, type **Dome9 Arc**, select **Dome9 Arc** from result panel then click **Add** button to add the application.</span></span>

    ![Dome9 Arc in the results list](./media/dome9arc-tutorial/tutorial_dome9arc_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="02adc-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="02adc-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="02adc-136">In this section, you configure and test Azure AD single sign-on with Dome9 Arc based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="02adc-136">In this section, you configure and test Azure AD single sign-on with Dome9 Arc based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="02adc-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Dome9 Arc is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02adc-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Dome9 Arc is to a user in Azure AD.</span></span> <span data-ttu-id="02adc-138">In other words, a link relationship between an Azure AD user and the related user in Dome9 Arc needs to be established.</span><span class="sxs-lookup"><span data-stu-id="02adc-138">In other words, a link relationship between an Azure AD user and the related user in Dome9 Arc needs to be established.</span></span>

<span data-ttu-id="02adc-139">To configure and test Azure AD single sign-on with Dome9 Arc, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="02adc-139">To configure and test Azure AD single sign-on with Dome9 Arc, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="02adc-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="02adc-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="02adc-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="02adc-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="02adc-142">**[Create a Dome9 Arc test user](#create-a-dome9-arc-test-user)** - to have a counterpart of Britta Simon in Dome9 Arc that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="02adc-142">**[Create a Dome9 Arc test user](#create-a-dome9-arc-test-user)** - to have a counterpart of Britta Simon in Dome9 Arc that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="02adc-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="02adc-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="02adc-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="02adc-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="02adc-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="02adc-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="02adc-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dome9 Arc application.</span><span class="sxs-lookup"><span data-stu-id="02adc-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dome9 Arc application.</span></span>

<span data-ttu-id="02adc-147">**To configure Azure AD single sign-on with Dome9 Arc, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="02adc-147">**To configure Azure AD single sign-on with Dome9 Arc, perform the following steps:**</span></span>

1. <span data-ttu-id="02adc-148">In the Azure portal, on the **Dome9 Arc** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="02adc-148">In the Azure portal, on the **Dome9 Arc** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="02adc-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="02adc-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/dome9arc-tutorial/tutorial_dome9arc_samlbase.png)

3. <span data-ttu-id="02adc-152">On the **Dome9 Arc Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="02adc-152">On the **Dome9 Arc Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Dome9 Arc Domain and URLs single sign-on information](./media/dome9arc-tutorial/tutorial_dome9arc_url.png)

    <span data-ttu-id="02adc-154">a.</span><span class="sxs-lookup"><span data-stu-id="02adc-154">a.</span></span> <span data-ttu-id="02adc-155">In the **Identifier** textbox, type the URL: `https://secure.dome9.com/`</span><span class="sxs-lookup"><span data-stu-id="02adc-155">In the **Identifier** textbox, type the URL: `https://secure.dome9.com/`</span></span>

    <span data-ttu-id="02adc-156">b.</span><span class="sxs-lookup"><span data-stu-id="02adc-156">b.</span></span> <span data-ttu-id="02adc-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://secure.dome9.com/sso/saml/yourcompanyname`</span><span class="sxs-lookup"><span data-stu-id="02adc-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://secure.dome9.com/sso/saml/yourcompanyname`</span></span>

    > [!NOTE]
    > <span data-ttu-id="02adc-158">You will select your company name value in the dome9 admin portal, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="02adc-158">You will select your company name value in the dome9 admin portal, which is explained later in the tutorial.</span></span>

4. <span data-ttu-id="02adc-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="02adc-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Dome9 Arc Domain and URLs single sign-on information](./media/dome9arc-tutorial/tutorial_dome9arc_url1.png)

    <span data-ttu-id="02adc-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://secure.dome9.com/sso/saml/<yourcompanyname>`</span><span class="sxs-lookup"><span data-stu-id="02adc-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://secure.dome9.com/sso/saml/<yourcompanyname>`</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="02adc-162">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="02adc-162">These values are not real.</span></span> <span data-ttu-id="02adc-163">Update these values with the actual Reply URL and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="02adc-163">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="02adc-164">Contact [Dome9 Arc Client support team](https://dome9.com/about/contact-us/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="02adc-164">Contact [Dome9 Arc Client support team](https://dome9.com/about/contact-us/) to get these values.</span></span> 

5. <span data-ttu-id="02adc-165">The Dome9 Arc Software application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="02adc-165">The Dome9 Arc Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="02adc-166">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="02adc-166">Configure the following claims for this application.</span></span> <span data-ttu-id="02adc-167">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="02adc-167">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="02adc-168">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="02adc-168">The following screenshot shows an example for this.</span></span>

    ![Configure Single Sign-On attb](./media/dome9arc-tutorial/tutorial_dome9arc_attribute.png)

6. <span data-ttu-id="02adc-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="02adc-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="02adc-171">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="02adc-171">Attribute Name</span></span>  | <span data-ttu-id="02adc-172">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="02adc-172">Attribute Value</span></span> | 
    | --------------- | --------------- | 
    | <span data-ttu-id="02adc-173">memberof</span><span class="sxs-lookup"><span data-stu-id="02adc-173">memberof</span></span> | <span data-ttu-id="02adc-174">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="02adc-174">user.assignedroles</span></span> |
    
    <span data-ttu-id="02adc-175">a.</span><span class="sxs-lookup"><span data-stu-id="02adc-175">a.</span></span> <span data-ttu-id="02adc-176">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="02adc-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On add attb](./media/dome9arc-tutorial/tutorial_dome9_04.png)

    ![Configure Single Sign-On edit attb](./media/dome9arc-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="02adc-179">b.</span><span class="sxs-lookup"><span data-stu-id="02adc-179">b.</span></span> <span data-ttu-id="02adc-180">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="02adc-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="02adc-181">c.</span><span class="sxs-lookup"><span data-stu-id="02adc-181">c.</span></span> <span data-ttu-id="02adc-182">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="02adc-182">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="02adc-183">d.</span><span class="sxs-lookup"><span data-stu-id="02adc-183">d.</span></span> <span data-ttu-id="02adc-184">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="02adc-184">Click **Ok**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="02adc-185">Please refer to this [link](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-enterprise-app-role-management) on how to configure and setup the roles for the application.</span><span class="sxs-lookup"><span data-stu-id="02adc-185">Please refer to this [link](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-enterprise-app-role-management) on how to configure and setup the roles for the application.</span></span>

7. <span data-ttu-id="02adc-186">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="02adc-186">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/dome9arc-tutorial/tutorial_dome9arc_certificate.png) 

8. <span data-ttu-id="02adc-188">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="02adc-188">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/dome9arc-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="02adc-190">On the **Dome9 Arc Configuration** section, click **Configure Dome9 Arc** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="02adc-190">On the **Dome9 Arc Configuration** section, click **Configure Dome9 Arc** to open **Configure sign-on** window.</span></span> <span data-ttu-id="02adc-191">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="02adc-191">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Dome9 Arc Configuration](./media/dome9arc-tutorial/tutorial_dome9arc_configure.png) 

10. <span data-ttu-id="02adc-193">In a different web browser window, log into your Dome9 Arc company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="02adc-193">In a different web browser window, log into your Dome9 Arc company site as an administrator.</span></span>

11. <span data-ttu-id="02adc-194">Click on the **Profile Settings** on the right top corner and then click **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="02adc-194">Click on the **Profile Settings** on the right top corner and then click **Account Settings**.</span></span> 

    ![Dome9 Arc Configuration](./media/dome9arc-tutorial/configure1.png)

12. <span data-ttu-id="02adc-196">Navigate to **SSO** and then click **ENABLE**.</span><span class="sxs-lookup"><span data-stu-id="02adc-196">Navigate to **SSO** and then click **ENABLE**.</span></span>

    ![Dome9 Arc Configuration](./media/dome9arc-tutorial/configure2.png)

13. <span data-ttu-id="02adc-198">In the SSO Configuration section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="02adc-198">In the SSO Configuration section, perform the following steps:</span></span>

    ![Dome9 Arc Configuration](./media/dome9arc-tutorial/configure3.png)

    <span data-ttu-id="02adc-200">a.</span><span class="sxs-lookup"><span data-stu-id="02adc-200">a.</span></span> <span data-ttu-id="02adc-201">Enter company name in the **Account ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="02adc-201">Enter company name in the **Account ID** textbox.</span></span> <span data-ttu-id="02adc-202">This value is to be used in the reply url mentioned in the Azure portal URL section.</span><span class="sxs-lookup"><span data-stu-id="02adc-202">This value is to be used in the reply url mentioned in the Azure portal URL section.</span></span>

    <span data-ttu-id="02adc-203">b.</span><span class="sxs-lookup"><span data-stu-id="02adc-203">b.</span></span> <span data-ttu-id="02adc-204">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied form the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="02adc-204">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied form the Azure portal.</span></span>

    <span data-ttu-id="02adc-205">c.</span><span class="sxs-lookup"><span data-stu-id="02adc-205">c.</span></span> <span data-ttu-id="02adc-206">In the **Idp endpoint url** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied form the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="02adc-206">In the **Idp endpoint url** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied form the Azure portal.</span></span>

    <span data-ttu-id="02adc-207">d.</span><span class="sxs-lookup"><span data-stu-id="02adc-207">d.</span></span> <span data-ttu-id="02adc-208">Open your downloaded Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="02adc-208">Open your downloaded Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 certificate** textbox.</span></span>

    <span data-ttu-id="02adc-209">e.</span><span class="sxs-lookup"><span data-stu-id="02adc-209">e.</span></span> <span data-ttu-id="02adc-210">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="02adc-210">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="02adc-211">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="02adc-211">Create an Azure AD test user</span></span>

<span data-ttu-id="02adc-212">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="02adc-212">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="02adc-214">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="02adc-214">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="02adc-215">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="02adc-215">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/dome9arc-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="02adc-217">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="02adc-217">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/dome9arc-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="02adc-219">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="02adc-219">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/dome9arc-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="02adc-221">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="02adc-221">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/dome9arc-tutorial/create_aaduser_04.png)

    <span data-ttu-id="02adc-223">a.</span><span class="sxs-lookup"><span data-stu-id="02adc-223">a.</span></span> <span data-ttu-id="02adc-224">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="02adc-224">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="02adc-225">b.</span><span class="sxs-lookup"><span data-stu-id="02adc-225">b.</span></span> <span data-ttu-id="02adc-226">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="02adc-226">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="02adc-227">c.</span><span class="sxs-lookup"><span data-stu-id="02adc-227">c.</span></span> <span data-ttu-id="02adc-228">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="02adc-228">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="02adc-229">d.</span><span class="sxs-lookup"><span data-stu-id="02adc-229">d.</span></span> <span data-ttu-id="02adc-230">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="02adc-230">Click **Create**.</span></span>

### <a name="create-a-dome9-arc-test-user"></a><span data-ttu-id="02adc-231">Create a Dome9 Arc test user</span><span class="sxs-lookup"><span data-stu-id="02adc-231">Create a Dome9 Arc test user</span></span>

<span data-ttu-id="02adc-232">To enable Azure AD users to log in to Dome9 Arc, they must be provisioned into application.</span><span class="sxs-lookup"><span data-stu-id="02adc-232">To enable Azure AD users to log in to Dome9 Arc, they must be provisioned into application.</span></span> <span data-ttu-id="02adc-233">Dome9 Arc supports just-in-time provisioning but for that to work properly, user have to select particular **Role** and assign the same to the user.</span><span class="sxs-lookup"><span data-stu-id="02adc-233">Dome9 Arc supports just-in-time provisioning but for that to work properly, user have to select particular **Role** and assign the same to the user.</span></span>

   >[!Note]
   ><span data-ttu-id="02adc-234">For **Role** creation and other details contact [Dome9 Arc Client support team](https://dome9.com/about/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="02adc-234">For **Role** creation and other details contact [Dome9 Arc Client support team](https://dome9.com/about/contact-us/).</span></span>

<span data-ttu-id="02adc-235">**To provision a user account manually, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="02adc-235">**To provision a user account manually, perform the following steps:**</span></span>

1. <span data-ttu-id="02adc-236">Log in to your Dome9 Arc company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="02adc-236">Log in to your Dome9 Arc company site as an administrator.</span></span>

2. <span data-ttu-id="02adc-237">Click on the **Users & Roles** and then click **Users**.</span><span class="sxs-lookup"><span data-stu-id="02adc-237">Click on the **Users & Roles** and then click **Users**.</span></span>

    ![Add Employee](./media/dome9arc-tutorial/user1.png)

3. <span data-ttu-id="02adc-239">Click **ADD USER**.</span><span class="sxs-lookup"><span data-stu-id="02adc-239">Click **ADD USER**.</span></span>

    ![Add Employee](./media/dome9arc-tutorial/user2.png)

4. <span data-ttu-id="02adc-241">In the **Create User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="02adc-241">In the **Create User** section, perform the following steps:</span></span>

    ![Add Employee](./media/dome9arc-tutorial/user3.png)

    <span data-ttu-id="02adc-243">a.</span><span class="sxs-lookup"><span data-stu-id="02adc-243">a.</span></span> <span data-ttu-id="02adc-244">In the **Email** textbox, type the email of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="02adc-244">In the **Email** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="02adc-245">b.</span><span class="sxs-lookup"><span data-stu-id="02adc-245">b.</span></span> <span data-ttu-id="02adc-246">In the **First Name** textbox, type first name of the user like Britta.</span><span class="sxs-lookup"><span data-stu-id="02adc-246">In the **First Name** textbox, type first name of the user like Britta.</span></span>

    <span data-ttu-id="02adc-247">c.</span><span class="sxs-lookup"><span data-stu-id="02adc-247">c.</span></span> <span data-ttu-id="02adc-248">In the **Last Name** textbox, type last name of the user like Simon.</span><span class="sxs-lookup"><span data-stu-id="02adc-248">In the **Last Name** textbox, type last name of the user like Simon.</span></span>

    <span data-ttu-id="02adc-249">d.</span><span class="sxs-lookup"><span data-stu-id="02adc-249">d.</span></span> <span data-ttu-id="02adc-250">Make **SSO User** as **On**.</span><span class="sxs-lookup"><span data-stu-id="02adc-250">Make **SSO User** as **On**.</span></span>

    <span data-ttu-id="02adc-251">e.</span><span class="sxs-lookup"><span data-stu-id="02adc-251">e.</span></span> <span data-ttu-id="02adc-252">Click **CREATE**.</span><span class="sxs-lookup"><span data-stu-id="02adc-252">Click **CREATE**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="02adc-253">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="02adc-253">Assign the Azure AD test user</span></span>

<span data-ttu-id="02adc-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dome9 Arc.</span><span class="sxs-lookup"><span data-stu-id="02adc-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dome9 Arc.</span></span>

![Assign the user role][200] 

<span data-ttu-id="02adc-256">**To assign Britta Simon to Dome9 Arc, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="02adc-256">**To assign Britta Simon to Dome9 Arc, perform the following steps:**</span></span>

1. <span data-ttu-id="02adc-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="02adc-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="02adc-259">In the applications list, select **Dome9 Arc**.</span><span class="sxs-lookup"><span data-stu-id="02adc-259">In the applications list, select **Dome9 Arc**.</span></span>

    ![The Dome9 Arc link in the Applications list](./media/dome9arc-tutorial/tutorial_dome9arc_app.png)  

3. <span data-ttu-id="02adc-261">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="02adc-261">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="02adc-263">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="02adc-263">Click **Add** button.</span></span> <span data-ttu-id="02adc-264">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="02adc-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="02adc-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="02adc-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="02adc-267">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="02adc-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="02adc-268">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="02adc-268">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="02adc-269">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="02adc-269">Test single sign-on</span></span>

<span data-ttu-id="02adc-270">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="02adc-270">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="02adc-271">When you click the Dome9 Arc tile in the Access Panel, you should get automatically signed-on to your Dome9 Arc application.</span><span class="sxs-lookup"><span data-stu-id="02adc-271">When you click the Dome9 Arc tile in the Access Panel, you should get automatically signed-on to your Dome9 Arc application.</span></span>
<span data-ttu-id="02adc-272">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="02adc-272">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="02adc-273">Additional resources</span><span class="sxs-lookup"><span data-stu-id="02adc-273">Additional resources</span></span>

* [<span data-ttu-id="02adc-274">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="02adc-274">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="02adc-275">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="02adc-275">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/dome9arc-tutorial/tutorial_general_01.png
[2]: ./media/dome9arc-tutorial/tutorial_general_02.png
[3]: ./media/dome9arc-tutorial/tutorial_general_03.png
[4]: ./media/dome9arc-tutorial/tutorial_general_04.png

[100]: ./media/dome9arc-tutorial/tutorial_general_100.png

[200]: ./media/dome9arc-tutorial/tutorial_general_200.png
[201]: ./media/dome9arc-tutorial/tutorial_general_201.png
[202]: ./media/dome9arc-tutorial/tutorial_general_202.png
[203]: ./media/dome9arc-tutorial/tutorial_general_203.png

