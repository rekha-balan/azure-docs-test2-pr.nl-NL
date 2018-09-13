---
title: 'Tutorial: Azure Active Directory integration with Vodeclic | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Vodeclic.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: d77a0f53-e3a3-445e-ab3e-119cef6e2e1d
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2017
ms.author: jeedes
ms.openlocfilehash: fb985b389139bfd8d54e6c54d101bbfa8a68a6d4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866301"
---
# <a name="tutorial-azure-active-directory-integration-with-vodeclic"></a><span data-ttu-id="a9a0f-103">Tutorial: Azure Active Directory integration with Vodeclic</span><span class="sxs-lookup"><span data-stu-id="a9a0f-103">Tutorial: Azure Active Directory integration with Vodeclic</span></span>

<span data-ttu-id="a9a0f-104">In this tutorial, you learn how to integrate Vodeclic with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a9a0f-104">In this tutorial, you learn how to integrate Vodeclic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a9a0f-105">Integrating Vodeclic with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a9a0f-105">Integrating Vodeclic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a9a0f-106">You can control in Azure AD who has access to Vodeclic.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-106">You can control in Azure AD who has access to Vodeclic.</span></span>
- <span data-ttu-id="a9a0f-107">You can enable your users to automatically get signed on to Vodeclic (single sign-on, or SSO) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-107">You can enable your users to automatically get signed on to Vodeclic (single sign-on, or SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a9a0f-108">You can manage your accounts in one central location--the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="a9a0f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a9a0f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9a0f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a9a0f-110">Prerequisites</span></span>

<span data-ttu-id="a9a0f-111">To configure Azure AD integration with Vodeclic, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a9a0f-111">To configure Azure AD integration with Vodeclic, you need the following items:</span></span>

- <span data-ttu-id="a9a0f-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a9a0f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a9a0f-113">A Vodeclic SSO-enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a9a0f-113">A Vodeclic SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a9a0f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a9a0f-115">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a9a0f-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="a9a0f-116">Don't use your production environment unless it's necessary.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="a9a0f-117">If you don't have an Azure AD trial environment, [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a9a0f-117">If you don't have an Azure AD trial environment, [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a9a0f-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a9a0f-118">Scenario description</span></span>
<span data-ttu-id="a9a0f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a9a0f-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a9a0f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a9a0f-121">Adding Vodeclic from the gallery</span><span class="sxs-lookup"><span data-stu-id="a9a0f-121">Adding Vodeclic from the gallery</span></span>
1. <span data-ttu-id="a9a0f-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a9a0f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-vodeclic-from-the-gallery"></a><span data-ttu-id="a9a0f-123">Add Vodeclic from the gallery</span><span class="sxs-lookup"><span data-stu-id="a9a0f-123">Add Vodeclic from the gallery</span></span>
<span data-ttu-id="a9a0f-124">To configure the integration of Vodeclic into Azure AD, you need to add Vodeclic from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-124">To configure the integration of Vodeclic into Azure AD, you need to add Vodeclic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a9a0f-125">**To add Vodeclic from the gallery, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9a0f-125">**To add Vodeclic from the gallery, take the following steps:**</span></span>

1. <span data-ttu-id="a9a0f-126">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-126">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="a9a0f-128">Go to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-128">Go to **Enterprise applications**.</span></span> <span data-ttu-id="a9a0f-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="a9a0f-131">To add a new application, select the **New application** button at the top of the dialog box.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-131">To add a new application, select the **New application** button at the top of the dialog box.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="a9a0f-133">In the search box, type **Vodeclic**.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-133">In the search box, type **Vodeclic**.</span></span> <span data-ttu-id="a9a0f-134">Select **Vodeclic** from the results panel, and then select the **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-134">Select **Vodeclic** from the results panel, and then select the **Add** button to add the application.</span></span>

    ![Vodeclic in the results list](./media/vodeclic-tutorial/tutorial_vodeclic_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a9a0f-136">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a9a0f-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a9a0f-137">In this section, you configure and test Azure AD single sign-on with Vodeclic based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a9a0f-137">In this section, you configure and test Azure AD single sign-on with Vodeclic based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a9a0f-138">For single sign-on to work, Azure AD needs to know who the counterpart user in Vodeclic is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-138">For single sign-on to work, Azure AD needs to know who the counterpart user in Vodeclic is to a user in Azure AD.</span></span> <span data-ttu-id="a9a0f-139">In other words, you need to establish a link between an Azure AD user and the related user in Vodeclic.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-139">In other words, you need to establish a link between an Azure AD user and the related user in Vodeclic.</span></span>

<span data-ttu-id="a9a0f-140">In Vodeclic, give the value **Username** the same value as **user name** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-140">In Vodeclic, give the value **Username** the same value as **user name** in Azure AD.</span></span> <span data-ttu-id="a9a0f-141">Now you have established the link between the two users.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-141">Now you have established the link between the two users.</span></span>

<span data-ttu-id="a9a0f-142">To configure and test Azure AD single sign-on with Vodeclic, complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a9a0f-142">To configure and test Azure AD single sign-on with Vodeclic, complete the following building blocks:</span></span>

1. <span data-ttu-id="a9a0f-143">[Configure Azure AD single sign-On](#configure-azure-ad-single-sign-on) to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-143">[Configure Azure AD single sign-On](#configure-azure-ad-single-sign-on) to enable your users to use this feature.</span></span>
1. <span data-ttu-id="a9a0f-144">[Create an Azure AD test user](#create-an-azure-ad-test-user) to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-144">[Create an Azure AD test user](#create-an-azure-ad-test-user) to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="a9a0f-145">[Create a Vodeclic test user](#create-a-vodeclic-test-user) to have a counterpart of Britta Simon in Vodeclic that is linked to the Azure AD representation of the user.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-145">[Create a Vodeclic test user](#create-a-vodeclic-test-user) to have a counterpart of Britta Simon in Vodeclic that is linked to the Azure AD representation of the user.</span></span>
1. <span data-ttu-id="a9a0f-146">[Assign the Azure AD test user](#assign-the-azure-ad-test-user) to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-146">[Assign the Azure AD test user](#assign-the-azure-ad-test-user) to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="a9a0f-147">[Test single sign-on](#test-single-sign-on) to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-147">[Test single sign-on](#test-single-sign-on) to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a9a0f-148">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a9a0f-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a9a0f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Vodeclic application.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Vodeclic application.</span></span>

<span data-ttu-id="a9a0f-150">**To configure Azure AD single sign-on with Vodeclic, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9a0f-150">**To configure Azure AD single sign-on with Vodeclic, take the following steps:**</span></span>

1. <span data-ttu-id="a9a0f-151">In the Azure portal, on the **Vodeclic** application integration page, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-151">In the Azure portal, on the **Vodeclic** application integration page, select **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="a9a0f-153">In the **Single sign-on** dialog box, under **Single-Sign-on Mode**, select **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-153">In the **Single sign-on** dialog box, under **Single-Sign-on Mode**, select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/vodeclic-tutorial/tutorial_vodeclic_samlbase.png)

1. <span data-ttu-id="a9a0f-155">If you want to configure the application in **IDP** initiated mode, in the **Vodeclic Domain and URLs** section, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="a9a0f-155">If you want to configure the application in **IDP** initiated mode, in the **Vodeclic Domain and URLs** section, take the following steps:</span></span>

    ![Vodeclic domain and URLs single sign-on information](./media/vodeclic-tutorial/tutorial_vodeclic_url.png)

    <span data-ttu-id="a9a0f-157">a.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-157">a.</span></span> <span data-ttu-id="a9a0f-158">In the **Identifier** box, type a URL with the following pattern: `https://<companyname>.lms.vodeclic.net/auth/saml`</span><span class="sxs-lookup"><span data-stu-id="a9a0f-158">In the **Identifier** box, type a URL with the following pattern: `https://<companyname>.lms.vodeclic.net/auth/saml`</span></span>

    <span data-ttu-id="a9a0f-159">b.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-159">b.</span></span> <span data-ttu-id="a9a0f-160">In the **Reply URL** box, type a URL with the following pattern: `https://<companyname>.lms.vodeclic.net/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="a9a0f-160">In the **Reply URL** box, type a URL with the following pattern: `https://<companyname>.lms.vodeclic.net/auth/saml/callback`</span></span>

1. <span data-ttu-id="a9a0f-161">If you want to configure the application in **SP** initiated mode, select the **Show advanced URL settings** check box, and take the following step:</span><span class="sxs-lookup"><span data-stu-id="a9a0f-161">If you want to configure the application in **SP** initiated mode, select the **Show advanced URL settings** check box, and take the following step:</span></span>

    ![Vodeclic domain and URLs single sign-on information](./media/vodeclic-tutorial/tutorial_vodeclic_url1.png)

    <span data-ttu-id="a9a0f-163">In the **Sign-on URL** box, type a URL with the following pattern: `https://<companyname>.lms.vodeclic.net/auth/saml`</span><span class="sxs-lookup"><span data-stu-id="a9a0f-163">In the **Sign-on URL** box, type a URL with the following pattern: `https://<companyname>.lms.vodeclic.net/auth/saml`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="a9a0f-164">These values aren't real.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-164">These values aren't real.</span></span> <span data-ttu-id="a9a0f-165">Update these values with the actual identifier, reply URL, and sign-on URL.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-165">Update these values with the actual identifier, reply URL, and sign-on URL.</span></span> <span data-ttu-id="a9a0f-166">Contact the [Vodeclic Client support team](mailto:hotline@vodeclic.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-166">Contact the [Vodeclic Client support team](mailto:hotline@vodeclic.com) to get these values.</span></span>

1. <span data-ttu-id="a9a0f-167">In the **SAML Signing Certificate** section, select **Metadata XML**.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-167">In the **SAML Signing Certificate** section, select **Metadata XML**.</span></span> <span data-ttu-id="a9a0f-168">Then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-168">Then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/vodeclic-tutorial/tutorial_vodeclic_certificate.png) 

1. <span data-ttu-id="a9a0f-170">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-170">Select **Save**.</span></span>

    ![Configure Single Sign-On Save button](./media/vodeclic-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="a9a0f-172">To configure single sign-on on the **Vodeclic** side, send the downloaded **Metadata XML** to the [Vodeclic support team](mailto:hotline@vodeclic.com).</span><span class="sxs-lookup"><span data-stu-id="a9a0f-172">To configure single sign-on on the **Vodeclic** side, send the downloaded **Metadata XML** to the [Vodeclic support team](mailto:hotline@vodeclic.com).</span></span> <span data-ttu-id="a9a0f-173">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-173">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a9a0f-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com) while you are setting up the app.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com) while you are setting up the app.</span></span> <span data-ttu-id="a9a0f-175">After you add this app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-175">After you add this app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a9a0f-176">You can read more about the embedded documentation feature at [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="a9a0f-176">You can read more about the embedded documentation feature at [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a9a0f-177">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a9a0f-177">Create an Azure AD test user</span></span>

<span data-ttu-id="a9a0f-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="a9a0f-180">**To create a test user in Azure AD, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9a0f-180">**To create a test user in Azure AD, take the following steps:**</span></span>

1. <span data-ttu-id="a9a0f-181">In the Azure portal, in the left pane, select the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-181">In the Azure portal, in the left pane, select the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/vodeclic-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="a9a0f-183">To display the list of users, go to **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-183">To display the list of users, go to **Users and groups**.</span></span> <span data-ttu-id="a9a0f-184">Then select **All users**.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-184">Then select **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/vodeclic-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="a9a0f-186">To open the **User** dialog box, select **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-186">To open the **User** dialog box, select **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/vodeclic-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="a9a0f-188">In the **User** dialog box, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="a9a0f-188">In the **User** dialog box, take the following steps:</span></span>

    ![The User dialog box](./media/vodeclic-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a9a0f-190">a.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-190">a.</span></span> <span data-ttu-id="a9a0f-191">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-191">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a9a0f-192">b.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-192">b.</span></span> <span data-ttu-id="a9a0f-193">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-193">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="a9a0f-194">c.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-194">c.</span></span> <span data-ttu-id="a9a0f-195">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-195">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="a9a0f-196">d.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-196">d.</span></span> <span data-ttu-id="a9a0f-197">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-197">Select **Create**.</span></span>
 
### <a name="create-a-vodeclic-test-user"></a><span data-ttu-id="a9a0f-198">Create a Vodeclic test user</span><span class="sxs-lookup"><span data-stu-id="a9a0f-198">Create a Vodeclic test user</span></span>

<span data-ttu-id="a9a0f-199">In this section, you create a user called Britta Simon in Vodeclic.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-199">In this section, you create a user called Britta Simon in Vodeclic.</span></span> <span data-ttu-id="a9a0f-200">Work with the [Vodeclic support team](mailto:hotline@vodeclic.com) to add the users in the Vodeclic platform.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-200">Work with the [Vodeclic support team](mailto:hotline@vodeclic.com) to add the users in the Vodeclic platform.</span></span> <span data-ttu-id="a9a0f-201">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-201">Users must be created and activated before you use single sign-on.</span></span>

> [!NOTE]
> <span data-ttu-id="a9a0f-202">According to application requirements, you might need to get your machine whitelisted.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-202">According to application requirements, you might need to get your machine whitelisted.</span></span> <span data-ttu-id="a9a0f-203">For that to happen, you need to share your public IP address with the [Vodeclic support team](mailto:hotline@vodeclic.com).</span><span class="sxs-lookup"><span data-stu-id="a9a0f-203">For that to happen, you need to share your public IP address with the [Vodeclic support team](mailto:hotline@vodeclic.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a9a0f-204">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a9a0f-204">Assign the Azure AD test user</span></span>

<span data-ttu-id="a9a0f-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Vodeclic.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Vodeclic.</span></span>

![Assign the user role][200] 

<span data-ttu-id="a9a0f-207">**To assign Britta Simon to Vodeclic, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9a0f-207">**To assign Britta Simon to Vodeclic, take the following steps:**</span></span>

1. <span data-ttu-id="a9a0f-208">In the Azure portal, open the applications view, and then go to the directory view.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-208">In the Azure portal, open the applications view, and then go to the directory view.</span></span> <span data-ttu-id="a9a0f-209">Next, go to **Enterprise applications**, and then select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-209">Next, go to **Enterprise applications**, and then select **All applications**.</span></span>

    ![Assign user][201] 

1. <span data-ttu-id="a9a0f-211">In the applications list, select **Vodeclic**.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-211">In the applications list, select **Vodeclic**.</span></span>

    ![The Vodeclic link in the Applications list](./media/vodeclic-tutorial/tutorial_vodeclic_app.png)  

1. <span data-ttu-id="a9a0f-213">In the menu on the left, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-213">In the menu on the left, select **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="a9a0f-215">Select the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-215">Select the **Add** button.</span></span> <span data-ttu-id="a9a0f-216">Then select **Users and groups** in the **Add Assignment** dialog box.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-216">Then select **Users and groups** in the **Add Assignment** dialog box.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="a9a0f-218">In the **Users and groups** dialog box, select **Britta Simon** in the **Users** list.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-218">In the **Users and groups** dialog box, select **Britta Simon** in the **Users** list.</span></span>

1. <span data-ttu-id="a9a0f-219">In the **Users and groups** dialog box, select the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-219">In the **Users and groups** dialog box, select the **Select** button.</span></span>

1. <span data-ttu-id="a9a0f-220">In the **Add Assignment** dialog box, select the **Assign** button.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-220">In the **Add Assignment** dialog box, select the **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a9a0f-221">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="a9a0f-221">Test single sign-on</span></span>

<span data-ttu-id="a9a0f-222">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-222">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span></span>

<span data-ttu-id="a9a0f-223">When you select the Vodeclic tile in the access panel, you get automatically signed in to your Vodeclic application.</span><span class="sxs-lookup"><span data-stu-id="a9a0f-223">When you select the Vodeclic tile in the access panel, you get automatically signed in to your Vodeclic application.</span></span>

<span data-ttu-id="a9a0f-224">For more information about the access panel, see [Introduction to the access panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a9a0f-224">For more information about the access panel, see [Introduction to the access panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a9a0f-225">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a9a0f-225">Additional resources</span></span>

* [<span data-ttu-id="a9a0f-226">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a9a0f-226">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a9a0f-227">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a9a0f-227">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/vodeclic-tutorial/tutorial_general_01.png
[2]: ./media/vodeclic-tutorial/tutorial_general_02.png
[3]: ./media/vodeclic-tutorial/tutorial_general_03.png
[4]: ./media/vodeclic-tutorial/tutorial_general_04.png

[100]: ./media/vodeclic-tutorial/tutorial_general_100.png

[200]: ./media/vodeclic-tutorial/tutorial_general_200.png
[201]: ./media/vodeclic-tutorial/tutorial_general_201.png
[202]: ./media/vodeclic-tutorial/tutorial_general_202.png
[203]: ./media/vodeclic-tutorial/tutorial_general_203.png

