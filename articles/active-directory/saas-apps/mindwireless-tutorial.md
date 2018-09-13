---
title: 'Tutorial: Azure Active Directory integration with mindWireless | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and mindWireless.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bd00a339-27c9-4904-b66f-a95bf597ac3c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/11/2018
ms.author: jeedes
ms.openlocfilehash: 6c6fe0a720795c67a7062f5a5971c699472fca07
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968806"
---
# <a name="tutorial-azure-active-directory-integration-with-mindwireless"></a><span data-ttu-id="34cb2-103">Tutorial: Azure Active Directory integration with mindWireless</span><span class="sxs-lookup"><span data-stu-id="34cb2-103">Tutorial: Azure Active Directory integration with mindWireless</span></span>

<span data-ttu-id="34cb2-104">In this tutorial, you learn how to integrate mindWireless with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="34cb2-104">In this tutorial, you learn how to integrate mindWireless with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="34cb2-105">Integrating mindWireless with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="34cb2-105">Integrating mindWireless with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="34cb2-106">You can control in Azure AD who has access to mindWireless.</span><span class="sxs-lookup"><span data-stu-id="34cb2-106">You can control in Azure AD who has access to mindWireless.</span></span>
- <span data-ttu-id="34cb2-107">You can enable your users to automatically get signed-on to mindWireless (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="34cb2-107">You can enable your users to automatically get signed-on to mindWireless (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="34cb2-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="34cb2-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="34cb2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="34cb2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34cb2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="34cb2-110">Prerequisites</span></span>

<span data-ttu-id="34cb2-111">To configure Azure AD integration with mindWireless, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="34cb2-111">To configure Azure AD integration with mindWireless, you need the following items:</span></span>

- <span data-ttu-id="34cb2-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="34cb2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="34cb2-113">A mindWireless single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="34cb2-113">A mindWireless single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="34cb2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="34cb2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="34cb2-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="34cb2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="34cb2-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="34cb2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="34cb2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="34cb2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="34cb2-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="34cb2-118">Scenario description</span></span>
<span data-ttu-id="34cb2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="34cb2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="34cb2-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="34cb2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="34cb2-121">Adding mindWireless from the gallery</span><span class="sxs-lookup"><span data-stu-id="34cb2-121">Adding mindWireless from the gallery</span></span>
1. <span data-ttu-id="34cb2-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="34cb2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mindwireless-from-the-gallery"></a><span data-ttu-id="34cb2-123">Adding mindWireless from the gallery</span><span class="sxs-lookup"><span data-stu-id="34cb2-123">Adding mindWireless from the gallery</span></span>
<span data-ttu-id="34cb2-124">To configure the integration of mindWireless into Azure AD, you need to add mindWireless from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="34cb2-124">To configure the integration of mindWireless into Azure AD, you need to add mindWireless from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="34cb2-125">**To add mindWireless from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="34cb2-125">**To add mindWireless from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="34cb2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="34cb2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="34cb2-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="34cb2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="34cb2-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="34cb2-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="34cb2-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="34cb2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="34cb2-133">In the search box, type **mindWireless**, select **mindWireless** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="34cb2-133">In the search box, type **mindWireless**, select **mindWireless** from result panel then click **Add** button to add the application.</span></span>

    ![mindWireless in the results list](./media/mindwireless-tutorial/tutorial_mindwireless_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="34cb2-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="34cb2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="34cb2-136">In this section, you configure and test Azure AD single sign-on with mindWireless based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="34cb2-136">In this section, you configure and test Azure AD single sign-on with mindWireless based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="34cb2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in mindWireless is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34cb2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in mindWireless is to a user in Azure AD.</span></span> <span data-ttu-id="34cb2-138">In other words, a link relationship between an Azure AD user and the related user in mindWireless needs to be established.</span><span class="sxs-lookup"><span data-stu-id="34cb2-138">In other words, a link relationship between an Azure AD user and the related user in mindWireless needs to be established.</span></span>

<span data-ttu-id="34cb2-139">To configure and test Azure AD single sign-on with mindWireless, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="34cb2-139">To configure and test Azure AD single sign-on with mindWireless, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="34cb2-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="34cb2-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="34cb2-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="34cb2-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="34cb2-142">**[Create a mindWireless test user](#create-a-mindwireless-test-user)** - to have a counterpart of Britta Simon in mindWireless that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="34cb2-142">**[Create a mindWireless test user](#create-a-mindwireless-test-user)** - to have a counterpart of Britta Simon in mindWireless that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="34cb2-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="34cb2-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="34cb2-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="34cb2-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="34cb2-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="34cb2-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="34cb2-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your mindWireless application.</span><span class="sxs-lookup"><span data-stu-id="34cb2-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your mindWireless application.</span></span>

<span data-ttu-id="34cb2-147">**To configure Azure AD single sign-on with mindWireless, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="34cb2-147">**To configure Azure AD single sign-on with mindWireless, perform the following steps:**</span></span>

1. <span data-ttu-id="34cb2-148">In the Azure portal, on the **mindWireless** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="34cb2-148">In the Azure portal, on the **mindWireless** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="34cb2-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="34cb2-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/mindwireless-tutorial/tutorial_mindwireless_samlbase.png)

1. <span data-ttu-id="34cb2-152">On the **mindWireless Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="34cb2-152">On the **mindWireless Domain and URLs** section, perform the following steps:</span></span>

    ![mindWireless Domain and URLs single sign-on information](./media/mindwireless-tutorial/tutorial_mindwireless_url.png)

    <span data-ttu-id="34cb2-154">a.</span><span class="sxs-lookup"><span data-stu-id="34cb2-154">a.</span></span> <span data-ttu-id="34cb2-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.mwsmart.com/`</span><span class="sxs-lookup"><span data-stu-id="34cb2-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.mwsmart.com/`</span></span>

    <span data-ttu-id="34cb2-156">b.</span><span class="sxs-lookup"><span data-stu-id="34cb2-156">b.</span></span> <span data-ttu-id="34cb2-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.mwsmart.com/SAML/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="34cb2-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.mwsmart.com/SAML/AssertionConsumerService.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="34cb2-158">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="34cb2-158">These values are not real.</span></span> <span data-ttu-id="34cb2-159">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="34cb2-159">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="34cb2-160">Contact [mindWireless support team](mailto:sdulloor@mindwireless.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="34cb2-160">Contact [mindWireless support team](mailto:sdulloor@mindwireless.com) to get these values.</span></span>

1. <span data-ttu-id="34cb2-161">The mindWireless application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="34cb2-161">The mindWireless application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span>

1. <span data-ttu-id="34cb2-162">The following screenshot shows an example for it.</span><span class="sxs-lookup"><span data-stu-id="34cb2-162">The following screenshot shows an example for it.</span></span> <span data-ttu-id="34cb2-163">The claim name always be **Employee ID** and the value of which we have mapped to user.employeeid, which contains the EmployeeID of the user.</span><span class="sxs-lookup"><span data-stu-id="34cb2-163">The claim name always be **Employee ID** and the value of which we have mapped to user.employeeid, which contains the EmployeeID of the user.</span></span> <span data-ttu-id="34cb2-164">Here the user mapping from Azure AD to mindWireless is done on the EmployeeID but you can map it to a different value also based on your application settings.</span><span class="sxs-lookup"><span data-stu-id="34cb2-164">Here the user mapping from Azure AD to mindWireless is done on the EmployeeID but you can map it to a different value also based on your application settings.</span></span> <span data-ttu-id="34cb2-165">You can work with the [mindWireless support team](mailto:sdulloor@mindwireless.com) first to use the correct identifier of a user and map that value with the **Employee ID** claim.</span><span class="sxs-lookup"><span data-stu-id="34cb2-165">You can work with the [mindWireless support team](mailto:sdulloor@mindwireless.com) first to use the correct identifier of a user and map that value with the **Employee ID** claim.</span></span>

    ![Configure Single Sign-On](./media/mindwireless-tutorial/tutorial_attribute.png)

1. <span data-ttu-id="34cb2-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="34cb2-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
    
    | <span data-ttu-id="34cb2-168">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="34cb2-168">Attribute Name</span></span> | <span data-ttu-id="34cb2-169">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="34cb2-169">Attribute Value</span></span> | <span data-ttu-id="34cb2-170">Namespace Value</span><span class="sxs-lookup"><span data-stu-id="34cb2-170">Namespace Value</span></span> |
    | -------------- | --------------- | ----------------|
    | <span data-ttu-id="34cb2-171">Employee ID</span><span class="sxs-lookup"><span data-stu-id="34cb2-171">Employee ID</span></span> | <span data-ttu-id="34cb2-172">user.employeeid</span><span class="sxs-lookup"><span data-stu-id="34cb2-172">user.employeeid</span></span> | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims`|
    
    <span data-ttu-id="34cb2-173">a.</span><span class="sxs-lookup"><span data-stu-id="34cb2-173">a.</span></span> <span data-ttu-id="34cb2-174">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="34cb2-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/mindwireless-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/mindwireless-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="34cb2-177">b.</span><span class="sxs-lookup"><span data-stu-id="34cb2-177">b.</span></span> <span data-ttu-id="34cb2-178">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="34cb2-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="34cb2-179">c.</span><span class="sxs-lookup"><span data-stu-id="34cb2-179">c.</span></span> <span data-ttu-id="34cb2-180">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="34cb2-180">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="34cb2-181">d.</span><span class="sxs-lookup"><span data-stu-id="34cb2-181">d.</span></span> <span data-ttu-id="34cb2-182">In the **Namespace** textbox, type the namespace value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="34cb2-182">In the **Namespace** textbox, type the namespace value shown for that row.</span></span>
    
    <span data-ttu-id="34cb2-183">e.</span><span class="sxs-lookup"><span data-stu-id="34cb2-183">e.</span></span> <span data-ttu-id="34cb2-184">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="34cb2-184">Click **Ok**.</span></span>
    
1. <span data-ttu-id="34cb2-185">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="34cb2-185">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/mindwireless-tutorial/tutorial_mindwireless_certificate.png) 

1. <span data-ttu-id="34cb2-187">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="34cb2-187">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/mindwireless-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="34cb2-189">On the **mindWireless Configuration** section, click **Configure mindWireless** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="34cb2-189">On the **mindWireless Configuration** section, click **Configure mindWireless** to open **Configure sign-on** window.</span></span> <span data-ttu-id="34cb2-190">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="34cb2-190">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![mindWireless Configuration](./media/mindwireless-tutorial/tutorial_mindwireless_configure.png) 

1. <span data-ttu-id="34cb2-192">To configure single sign-on on **mindWireless** side, you need to send the downloaded **Certificate(Base64), SAML Single Sign-On Service URL**, and **SAML Entity ID** to [mindWireless support team](mailto:sdulloor@mindwireless.com).</span><span class="sxs-lookup"><span data-stu-id="34cb2-192">To configure single sign-on on **mindWireless** side, you need to send the downloaded **Certificate(Base64), SAML Single Sign-On Service URL**, and **SAML Entity ID** to [mindWireless support team](mailto:sdulloor@mindwireless.com).</span></span> <span data-ttu-id="34cb2-193">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="34cb2-193">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="34cb2-194">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="34cb2-194">Create an Azure AD test user</span></span>

<span data-ttu-id="34cb2-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="34cb2-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="34cb2-197">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="34cb2-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="34cb2-198">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="34cb2-198">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/mindwireless-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="34cb2-200">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="34cb2-200">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/mindwireless-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="34cb2-202">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="34cb2-202">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/mindwireless-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="34cb2-204">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="34cb2-204">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/mindwireless-tutorial/create_aaduser_04.png)

    <span data-ttu-id="34cb2-206">a.</span><span class="sxs-lookup"><span data-stu-id="34cb2-206">a.</span></span> <span data-ttu-id="34cb2-207">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="34cb2-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="34cb2-208">b.</span><span class="sxs-lookup"><span data-stu-id="34cb2-208">b.</span></span> <span data-ttu-id="34cb2-209">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="34cb2-209">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="34cb2-210">c.</span><span class="sxs-lookup"><span data-stu-id="34cb2-210">c.</span></span> <span data-ttu-id="34cb2-211">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="34cb2-211">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="34cb2-212">d.</span><span class="sxs-lookup"><span data-stu-id="34cb2-212">d.</span></span> <span data-ttu-id="34cb2-213">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="34cb2-213">Click **Create**.</span></span>

### <a name="create-a-mindwireless-test-user"></a><span data-ttu-id="34cb2-214">Create a mindWireless test user</span><span class="sxs-lookup"><span data-stu-id="34cb2-214">Create a mindWireless test user</span></span>

<span data-ttu-id="34cb2-215">In this section, you create a user called Britta Simon in mindWireless.</span><span class="sxs-lookup"><span data-stu-id="34cb2-215">In this section, you create a user called Britta Simon in mindWireless.</span></span> <span data-ttu-id="34cb2-216">Work with [mindWireless support team](mailto:sdulloor@mindwireless.com) to add the users in the mindWireless platform.</span><span class="sxs-lookup"><span data-stu-id="34cb2-216">Work with [mindWireless support team](mailto:sdulloor@mindwireless.com) to add the users in the mindWireless platform.</span></span> <span data-ttu-id="34cb2-217">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="34cb2-217">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="34cb2-218">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="34cb2-218">Assign the Azure AD test user</span></span>

<span data-ttu-id="34cb2-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to mindWireless.</span><span class="sxs-lookup"><span data-stu-id="34cb2-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to mindWireless.</span></span>

![Assign the user role][200] 

<span data-ttu-id="34cb2-221">**To assign Britta Simon to mindWireless, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="34cb2-221">**To assign Britta Simon to mindWireless, perform the following steps:**</span></span>

1. <span data-ttu-id="34cb2-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="34cb2-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="34cb2-224">In the applications list, select **mindWireless**.</span><span class="sxs-lookup"><span data-stu-id="34cb2-224">In the applications list, select **mindWireless**.</span></span>

    ![The mindWireless link in the Applications list](./media/mindwireless-tutorial/tutorial_mindwireless_app.png)  

1. <span data-ttu-id="34cb2-226">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="34cb2-226">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="34cb2-228">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="34cb2-228">Click **Add** button.</span></span> <span data-ttu-id="34cb2-229">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="34cb2-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="34cb2-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="34cb2-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="34cb2-232">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="34cb2-232">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="34cb2-233">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="34cb2-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="34cb2-234">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="34cb2-234">Test single sign-on</span></span>

<span data-ttu-id="34cb2-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="34cb2-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="34cb2-236">When you click the mindWireless tile in the Access Panel, you should get automatically signed-on to your mindWireless application.</span><span class="sxs-lookup"><span data-stu-id="34cb2-236">When you click the mindWireless tile in the Access Panel, you should get automatically signed-on to your mindWireless application.</span></span>
<span data-ttu-id="34cb2-237">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="34cb2-237">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="34cb2-238">Additional resources</span><span class="sxs-lookup"><span data-stu-id="34cb2-238">Additional resources</span></span>

* [<span data-ttu-id="34cb2-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34cb2-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="34cb2-240">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="34cb2-240">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/mindwireless-tutorial/tutorial_general_01.png
[2]: ./media/mindwireless-tutorial/tutorial_general_02.png
[3]: ./media/mindwireless-tutorial/tutorial_general_03.png
[4]: ./media/mindwireless-tutorial/tutorial_general_04.png

[100]: ./media/mindwireless-tutorial/tutorial_general_100.png

[200]: ./media/mindwireless-tutorial/tutorial_general_200.png
[201]: ./media/mindwireless-tutorial/tutorial_general_201.png
[202]: ./media/mindwireless-tutorial/tutorial_general_202.png
[203]: ./media/mindwireless-tutorial/tutorial_general_203.png

