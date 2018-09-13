---
title: 'Tutorial: Azure Active Directory integration with OpenAthens | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and OpenAthens.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: dd4adfc7-e238-41d5-8b25-1811f08078b6
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/05/2017
ms.author: jeedes
ms.openlocfilehash: 269b216a94b1233c5f9f9a634fda3c05e46cac90
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870316"
---
# <a name="tutorial-azure-active-directory-integration-with-openathens"></a><span data-ttu-id="c85e7-103">Tutorial: Azure Active Directory integration with OpenAthens</span><span class="sxs-lookup"><span data-stu-id="c85e7-103">Tutorial: Azure Active Directory integration with OpenAthens</span></span>

<span data-ttu-id="c85e7-104">In this tutorial, you learn how to integrate OpenAthens with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c85e7-104">In this tutorial, you learn how to integrate OpenAthens with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c85e7-105">Integrating OpenAthens with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="c85e7-105">Integrating OpenAthens with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c85e7-106">You can control in Azure AD who has access to OpenAthens.</span><span class="sxs-lookup"><span data-stu-id="c85e7-106">You can control in Azure AD who has access to OpenAthens.</span></span>
- <span data-ttu-id="c85e7-107">You can enable your users to automatically sign on to OpenAthens (single sign-on) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="c85e7-107">You can enable your users to automatically sign on to OpenAthens (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c85e7-108">You can manage your accounts in one central location--the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c85e7-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="c85e7-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="c85e7-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c85e7-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c85e7-110">Prerequisites</span></span>

<span data-ttu-id="c85e7-111">To configure Azure AD integration with OpenAthens, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="c85e7-111">To configure Azure AD integration with OpenAthens, you need the following items:</span></span>

- <span data-ttu-id="c85e7-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="c85e7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c85e7-113">An OpenAthens single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="c85e7-113">An OpenAthens single sign-on enabled subscription</span></span>

<span data-ttu-id="c85e7-114">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="c85e7-114">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c85e7-115">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="c85e7-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c85e7-116">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c85e7-116">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c85e7-117">Scenario description</span><span class="sxs-lookup"><span data-stu-id="c85e7-117">Scenario description</span></span>
<span data-ttu-id="c85e7-118">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="c85e7-118">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c85e7-119">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="c85e7-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c85e7-120">Adding OpenAthens from the gallery</span><span class="sxs-lookup"><span data-stu-id="c85e7-120">Adding OpenAthens from the gallery</span></span>
1. <span data-ttu-id="c85e7-121">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c85e7-121">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-openathens-from-the-gallery"></a><span data-ttu-id="c85e7-122">Adding OpenAthens from the gallery</span><span class="sxs-lookup"><span data-stu-id="c85e7-122">Adding OpenAthens from the gallery</span></span>
<span data-ttu-id="c85e7-123">To configure the integration of OpenAthens into Azure AD, you need to add OpenAthens from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="c85e7-123">To configure the integration of OpenAthens into Azure AD, you need to add OpenAthens from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c85e7-124">**To add OpenAthens from the gallery**</span><span class="sxs-lookup"><span data-stu-id="c85e7-124">**To add OpenAthens from the gallery**</span></span>

1. <span data-ttu-id="c85e7-125">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="c85e7-125">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="c85e7-127">Browse to **Enterprise applications**, and then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c85e7-127">Browse to **Enterprise applications**, and then go to **All applications**.</span></span>

    ![The Enterprise applications pane][2]
    
1. <span data-ttu-id="c85e7-129">To add new application, select the **New application** button on the top of the dialog box.</span><span class="sxs-lookup"><span data-stu-id="c85e7-129">To add new application, select the **New application** button on the top of the dialog box.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="c85e7-131">In the search box, type **OpenAthens**, select **OpenAthens** from the results panel, and then select the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="c85e7-131">In the search box, type **OpenAthens**, select **OpenAthens** from the results panel, and then select the **Add** button.</span></span>

    ![OpenAthens in the results list](./media/openathens-tutorial/tutorial_openathens_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c85e7-133">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c85e7-133">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c85e7-134">In this section, you configure and test Azure AD single sign-on with OpenAthens based on a test user named "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="c85e7-134">In this section, you configure and test Azure AD single sign-on with OpenAthens based on a test user named "Britta Simon."</span></span>

<span data-ttu-id="c85e7-135">For single sign-on to work, Azure AD needs to know what the counterpart user in OpenAthens is to the user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c85e7-135">For single sign-on to work, Azure AD needs to know what the counterpart user in OpenAthens is to the user in Azure AD.</span></span> <span data-ttu-id="c85e7-136">In other words, you need to establish a link relationship between an Azure AD user and the related user in OpenAthens.</span><span class="sxs-lookup"><span data-stu-id="c85e7-136">In other words, you need to establish a link relationship between an Azure AD user and the related user in OpenAthens.</span></span>

<span data-ttu-id="c85e7-137">In OpenAthens, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="c85e7-137">In OpenAthens, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c85e7-138">To configure and test Azure AD single sign-on with OpenAthens, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c85e7-138">To configure and test Azure AD single sign-on with OpenAthens, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c85e7-139">[Configure Azure AD single sign-On](#configure-azure-ad-single-sign-on), to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c85e7-139">[Configure Azure AD single sign-On](#configure-azure-ad-single-sign-on), to enable your users to use this feature.</span></span>
1. <span data-ttu-id="c85e7-140">[Create an Azure AD test user](#create-an-azure-ad-test-user), to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c85e7-140">[Create an Azure AD test user](#create-an-azure-ad-test-user), to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="c85e7-141">[Create an OpenAthens test user](#create-a-openathens-test-user), to have a counterpart of Britta Simon in OpenAthens that is linked to the Azure AD representation of the user.</span><span class="sxs-lookup"><span data-stu-id="c85e7-141">[Create an OpenAthens test user](#create-a-openathens-test-user), to have a counterpart of Britta Simon in OpenAthens that is linked to the Azure AD representation of the user.</span></span>
1. <span data-ttu-id="c85e7-142">[Assign the Azure AD test user](#assign-the-azure-ad-test-user), to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c85e7-142">[Assign the Azure AD test user](#assign-the-azure-ad-test-user), to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="c85e7-143">[Test single sign-on](#test-single-sign-on), to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="c85e7-143">[Test single sign-on](#test-single-sign-on), to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c85e7-144">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c85e7-144">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c85e7-145">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OpenAthens application.</span><span class="sxs-lookup"><span data-stu-id="c85e7-145">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OpenAthens application.</span></span>

<span data-ttu-id="c85e7-146">**To configure Azure AD single sign-on with OpenAthens**</span><span class="sxs-lookup"><span data-stu-id="c85e7-146">**To configure Azure AD single sign-on with OpenAthens**</span></span>

1. <span data-ttu-id="c85e7-147">In the Azure portal, on the **OpenAthens** application integration page, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c85e7-147">In the Azure portal, on the **OpenAthens** application integration page, select **Single sign-on**.</span></span>

    ![Configure the single sign-on link][4]

1. <span data-ttu-id="c85e7-149">To enable single sign-on, in the **Single sign-on** dialog box, select **SAML-based Sign-on** as the **Mode**.</span><span class="sxs-lookup"><span data-stu-id="c85e7-149">To enable single sign-on, in the **Single sign-on** dialog box, select **SAML-based Sign-on** as the **Mode**.</span></span>
 
    ![Single sign-on dialog box](./media/openathens-tutorial/tutorial_openathens_samlbase.png)

1. <span data-ttu-id="c85e7-151">In the **OpenAthens Domain and URLs** section, enter the value `https://login.openathens.net/saml/2/metadata-sp` in the **Identifier** text box.</span><span class="sxs-lookup"><span data-stu-id="c85e7-151">In the **OpenAthens Domain and URLs** section, enter the value `https://login.openathens.net/saml/2/metadata-sp` in the **Identifier** text box.</span></span>

    ![OpenAthens domain and URLs single sign-on information](./media/openathens-tutorial/tutorial_openathens_url.png)

1. <span data-ttu-id="c85e7-153">In the **SAML Signing Certificate** section, select **Metadata XML**, and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="c85e7-153">In the **SAML Signing Certificate** section, select **Metadata XML**, and then save the metadata file on your computer.</span></span>

    ![The AMSL Signing Certificate download link](./media/openathens-tutorial/tutorial_openathens_certificate.png) 

1. <span data-ttu-id="c85e7-155">Select the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="c85e7-155">Select the **Save** button.</span></span>

    ![The single sign-on Save button](./media/openathens-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="c85e7-157">In a different web browser window, log in to your OpenAthens company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c85e7-157">In a different web browser window, log in to your OpenAthens company site as an administrator.</span></span>

1. <span data-ttu-id="c85e7-158">Select **Connections** from the list under the **Management** tab.</span><span class="sxs-lookup"><span data-stu-id="c85e7-158">Select **Connections** from the list under the **Management** tab.</span></span> 

    ![Configure single sign-on](./media/openathens-tutorial/tutorial_openathens_application1.png)

1. <span data-ttu-id="c85e7-160">Select **SAML 1.1/2.0**, and then select the **Configure** button.</span><span class="sxs-lookup"><span data-stu-id="c85e7-160">Select **SAML 1.1/2.0**, and then select the **Configure** button.</span></span>

    ![Configure single sign-on](./media/openathens-tutorial/tutorial_openathens_application2.png)
    
1. <span data-ttu-id="c85e7-162">To add the configuration, select the **Browse** button to upload the metadata .xml file that you downloaded from the Azure portal, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="c85e7-162">To add the configuration, select the **Browse** button to upload the metadata .xml file that you downloaded from the Azure portal, and then select **Add**.</span></span>

    ![Configure single sign-on](./media/openathens-tutorial/tutorial_openathens_application3.png)

1. <span data-ttu-id="c85e7-164">Perform the following steps under the **Details** tab.</span><span class="sxs-lookup"><span data-stu-id="c85e7-164">Perform the following steps under the **Details** tab.</span></span>

    ![Configure single sign-on](./media/openathens-tutorial/tutorial_openathens_application4.png)

    <span data-ttu-id="c85e7-166">a.</span><span class="sxs-lookup"><span data-stu-id="c85e7-166">a.</span></span> <span data-ttu-id="c85e7-167">In **Display name mapping**, select **Use attribute**.</span><span class="sxs-lookup"><span data-stu-id="c85e7-167">In **Display name mapping**, select **Use attribute**.</span></span>

    <span data-ttu-id="c85e7-168">b.</span><span class="sxs-lookup"><span data-stu-id="c85e7-168">b.</span></span> <span data-ttu-id="c85e7-169">In the **Display name attribute** text box, enter the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="c85e7-169">In the **Display name attribute** text box, enter the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="c85e7-170">c.</span><span class="sxs-lookup"><span data-stu-id="c85e7-170">c.</span></span> <span data-ttu-id="c85e7-171">In **Unique user mapping**, select **Use attribute**.</span><span class="sxs-lookup"><span data-stu-id="c85e7-171">In **Unique user mapping**, select **Use attribute**.</span></span>

    <span data-ttu-id="c85e7-172">d.</span><span class="sxs-lookup"><span data-stu-id="c85e7-172">d.</span></span> <span data-ttu-id="c85e7-173">In the **Unique user attribute** text box, enter the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="c85e7-173">In the **Unique user attribute** text box, enter the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="c85e7-174">e.</span><span class="sxs-lookup"><span data-stu-id="c85e7-174">e.</span></span> <span data-ttu-id="c85e7-175">In **Status**, select all the three check boxes.</span><span class="sxs-lookup"><span data-stu-id="c85e7-175">In **Status**, select all the three check boxes.</span></span>

    <span data-ttu-id="c85e7-176">f.</span><span class="sxs-lookup"><span data-stu-id="c85e7-176">f.</span></span> <span data-ttu-id="c85e7-177">In **Create local accounts**, select **automatically**.</span><span class="sxs-lookup"><span data-stu-id="c85e7-177">In **Create local accounts**, select **automatically**.</span></span>

    <span data-ttu-id="c85e7-178">g.</span><span class="sxs-lookup"><span data-stu-id="c85e7-178">g.</span></span> <span data-ttu-id="c85e7-179">Select **Save changes**.</span><span class="sxs-lookup"><span data-stu-id="c85e7-179">Select **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="c85e7-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app.</span><span class="sxs-lookup"><span data-stu-id="c85e7-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app.</span></span> <span data-ttu-id="c85e7-181">After you add this app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="c85e7-181">After you add this app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c85e7-182">For more about the embedded documentation feature, see the [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="c85e7-182">For more about the embedded documentation feature, see the [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c85e7-183">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c85e7-183">Create an Azure AD test user</span></span>

<span data-ttu-id="c85e7-184">The objective of this section is to create a test user in the Azure portal called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="c85e7-184">The objective of this section is to create a test user in the Azure portal called "Britta Simon."</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="c85e7-186">**To create a test user in Azure AD**</span><span class="sxs-lookup"><span data-stu-id="c85e7-186">**To create a test user in Azure AD**</span></span>

1. <span data-ttu-id="c85e7-187">In the Azure portal, in the left pane, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c85e7-187">In the Azure portal, in the left pane, select **Azure Active Directory**.</span></span>

    ![The Azure Active Directory button](./media/openathens-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="c85e7-189">To display the list of users, go to **Users and groups**, and then select **All users**.</span><span class="sxs-lookup"><span data-stu-id="c85e7-189">To display the list of users, go to **Users and groups**, and then select **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/openathens-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="c85e7-191">To open the **User** dialog box, select **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="c85e7-191">To open the **User** dialog box, select **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/openathens-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="c85e7-193">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c85e7-193">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/openathens-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c85e7-195">a.</span><span class="sxs-lookup"><span data-stu-id="c85e7-195">a.</span></span> <span data-ttu-id="c85e7-196">In the **Name** text box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c85e7-196">In the **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c85e7-197">b.</span><span class="sxs-lookup"><span data-stu-id="c85e7-197">b.</span></span> <span data-ttu-id="c85e7-198">In the **User name** text box, type the email address for Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c85e7-198">In the **User name** text box, type the email address for Britta Simon.</span></span>

    <span data-ttu-id="c85e7-199">c.</span><span class="sxs-lookup"><span data-stu-id="c85e7-199">c.</span></span> <span data-ttu-id="c85e7-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** text box.</span><span class="sxs-lookup"><span data-stu-id="c85e7-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** text box.</span></span>

    <span data-ttu-id="c85e7-201">d.</span><span class="sxs-lookup"><span data-stu-id="c85e7-201">d.</span></span> <span data-ttu-id="c85e7-202">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="c85e7-202">Select **Create**.</span></span>
  
### <a name="create-an-openathens-test-user"></a><span data-ttu-id="c85e7-203">Create an OpenAthens test user</span><span class="sxs-lookup"><span data-stu-id="c85e7-203">Create an OpenAthens test user</span></span>

<span data-ttu-id="c85e7-204">OpenAthens supports just-in-time provisioning, and users are created automatically after successful authentication.</span><span class="sxs-lookup"><span data-stu-id="c85e7-204">OpenAthens supports just-in-time provisioning, and users are created automatically after successful authentication.</span></span> <span data-ttu-id="c85e7-205">You don't need to perform any action in this section.</span><span class="sxs-lookup"><span data-stu-id="c85e7-205">You don't need to perform any action in this section.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c85e7-206">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c85e7-206">Assign the Azure AD test user</span></span>

<span data-ttu-id="c85e7-207">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to OpenAthens.</span><span class="sxs-lookup"><span data-stu-id="c85e7-207">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to OpenAthens.</span></span>

![Assign the user role][200] 

<span data-ttu-id="c85e7-209">**To assign Britta Simon to OpenAthens**</span><span class="sxs-lookup"><span data-stu-id="c85e7-209">**To assign Britta Simon to OpenAthens**</span></span>

1. <span data-ttu-id="c85e7-210">In the Azure portal, open the applications view, browse to the directory view and go to **Enterprise applications**, and then select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c85e7-210">In the Azure portal, open the applications view, browse to the directory view and go to **Enterprise applications**, and then select **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="c85e7-212">In the **Applications** list, select **OpenAthens**.</span><span class="sxs-lookup"><span data-stu-id="c85e7-212">In the **Applications** list, select **OpenAthens**.</span></span>

    ![The OpenAthens link in the Applications list](./media/openathens-tutorial/tutorial_openathens_app.png)  

1. <span data-ttu-id="c85e7-214">In the menu on the left, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="c85e7-214">In the menu on the left, select **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="c85e7-216">Select the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="c85e7-216">Select the **Add** button.</span></span> <span data-ttu-id="c85e7-217">Then select **Users and groups** in the **Add Assignment** pane.</span><span class="sxs-lookup"><span data-stu-id="c85e7-217">Then select **Users and groups** in the **Add Assignment** pane.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="c85e7-219">In the **Users and groups** list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c85e7-219">In the **Users and groups** list, select **Britta Simon**.</span></span>

1. <span data-ttu-id="c85e7-220">Select the **Select** button in the **Users and groups** list.</span><span class="sxs-lookup"><span data-stu-id="c85e7-220">Select the **Select** button in the **Users and groups** list.</span></span>

1. <span data-ttu-id="c85e7-221">Select the **Assign** button in the **Add Assignment** pane.</span><span class="sxs-lookup"><span data-stu-id="c85e7-221">Select the **Assign** button in the **Add Assignment** pane.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c85e7-222">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="c85e7-222">Test single sign-on</span></span>

<span data-ttu-id="c85e7-223">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c85e7-223">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="c85e7-224">When you select the **OpenAthens** tile in the Access Panel, you should be automatically signed on to your OpenAthens application.</span><span class="sxs-lookup"><span data-stu-id="c85e7-224">When you select the **OpenAthens** tile in the Access Panel, you should be automatically signed on to your OpenAthens application.</span></span>
<span data-ttu-id="c85e7-225">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c85e7-225">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c85e7-226">Additional resources</span><span class="sxs-lookup"><span data-stu-id="c85e7-226">Additional resources</span></span>

* <span data-ttu-id="c85e7-227">For a list of tutorials on how to integrate SaaS apps with Azure Active Directory, see [SaaS app integration tutorials for use with Azure AD](tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="c85e7-227">For a list of tutorials on how to integrate SaaS apps with Azure Active Directory, see [SaaS app integration tutorials for use with Azure AD](tutorial-list.md).</span></span>
* <span data-ttu-id="c85e7-228">For more information about application access and single sign-on with Azure Active Directory, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="c85e7-228">For more information about application access and single sign-on with Azure Active Directory, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

<!--Image references-->

[1]: ./media/openathens-tutorial/tutorial_general_01.png
[2]: ./media/openathens-tutorial/tutorial_general_02.png
[3]: ./media/openathens-tutorial/tutorial_general_03.png
[4]: ./media/openathens-tutorial/tutorial_general_04.png

[100]: ./media/openathens-tutorial/tutorial_general_100.png

[200]: ./media/openathens-tutorial/tutorial_general_200.png
[201]: ./media/openathens-tutorial/tutorial_general_201.png
[202]: ./media/openathens-tutorial/tutorial_general_202.png
[203]: ./media/openathens-tutorial/tutorial_general_203.png

