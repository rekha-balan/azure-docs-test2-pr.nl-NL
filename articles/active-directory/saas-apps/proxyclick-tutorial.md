---
title: 'Tutorial: Azure Active Directory integration with Proxyclick | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Proxyclick.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5c58a859-71c2-4542-ae92-e5f16a8e7f18
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/21/2018
ms.author: jeedes
ms.openlocfilehash: d93c5486d9c23558995742fc27e1222834cf4452
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866299"
---
# <a name="tutorial-azure-active-directory-integration-with-proxyclick"></a><span data-ttu-id="2f343-103">Tutorial: Azure Active Directory integration with Proxyclick</span><span class="sxs-lookup"><span data-stu-id="2f343-103">Tutorial: Azure Active Directory integration with Proxyclick</span></span>

<span data-ttu-id="2f343-104">In this tutorial, you learn how to integrate Proxyclick with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2f343-104">In this tutorial, you learn how to integrate Proxyclick with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f343-105">Integrating Proxyclick with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="2f343-105">Integrating Proxyclick with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2f343-106">You can control in Azure AD who has access to Proxyclick.</span><span class="sxs-lookup"><span data-stu-id="2f343-106">You can control in Azure AD who has access to Proxyclick.</span></span>
- <span data-ttu-id="2f343-107">You can enable your users to automatically get signed-on to Proxyclick (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="2f343-107">You can enable your users to automatically get signed-on to Proxyclick (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2f343-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2f343-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="2f343-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="2f343-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f343-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2f343-110">Prerequisites</span></span>

<span data-ttu-id="2f343-111">To configure Azure AD integration with Proxyclick, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="2f343-111">To configure Azure AD integration with Proxyclick, you need the following items:</span></span>

- <span data-ttu-id="2f343-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="2f343-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2f343-113">A Proxyclick single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="2f343-113">A Proxyclick single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2f343-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="2f343-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2f343-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="2f343-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2f343-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="2f343-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2f343-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f343-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2f343-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="2f343-118">Scenario description</span></span>
<span data-ttu-id="2f343-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="2f343-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2f343-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="2f343-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2f343-121">Adding Proxyclick from the gallery</span><span class="sxs-lookup"><span data-stu-id="2f343-121">Adding Proxyclick from the gallery</span></span>
1. <span data-ttu-id="2f343-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2f343-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-proxyclick-from-the-gallery"></a><span data-ttu-id="2f343-123">Adding Proxyclick from the gallery</span><span class="sxs-lookup"><span data-stu-id="2f343-123">Adding Proxyclick from the gallery</span></span>
<span data-ttu-id="2f343-124">To configure the integration of Proxyclick into Azure AD, you need to add Proxyclick from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="2f343-124">To configure the integration of Proxyclick into Azure AD, you need to add Proxyclick from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2f343-125">**To add Proxyclick from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2f343-125">**To add Proxyclick from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2f343-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="2f343-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="2f343-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="2f343-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2f343-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2f343-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="2f343-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="2f343-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="2f343-133">In the search box, type **Proxyclick**, select **Proxyclick** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="2f343-133">In the search box, type **Proxyclick**, select **Proxyclick** from result panel then click **Add** button to add the application.</span></span>

    ![Proxyclick in the results list](./media/proxyclick-tutorial/tutorial_proxyclick_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2f343-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2f343-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2f343-136">In this section, you configure and test Azure AD single sign-on with Proxyclick based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2f343-136">In this section, you configure and test Azure AD single sign-on with Proxyclick based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2f343-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Proxyclick is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f343-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Proxyclick is to a user in Azure AD.</span></span> <span data-ttu-id="2f343-138">In other words, a link relationship between an Azure AD user and the related user in Proxyclick needs to be established.</span><span class="sxs-lookup"><span data-stu-id="2f343-138">In other words, a link relationship between an Azure AD user and the related user in Proxyclick needs to be established.</span></span>

<span data-ttu-id="2f343-139">To configure and test Azure AD single sign-on with Proxyclick, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="2f343-139">To configure and test Azure AD single sign-on with Proxyclick, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2f343-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="2f343-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="2f343-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2f343-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="2f343-142">**[Create a Proxyclick test user](#create-a-proxyclick-test-user)** - to have a counterpart of Britta Simon in Proxyclick that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="2f343-142">**[Create a Proxyclick test user](#create-a-proxyclick-test-user)** - to have a counterpart of Britta Simon in Proxyclick that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="2f343-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2f343-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="2f343-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="2f343-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2f343-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2f343-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2f343-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Proxyclick application.</span><span class="sxs-lookup"><span data-stu-id="2f343-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Proxyclick application.</span></span>

<span data-ttu-id="2f343-147">**To configure Azure AD single sign-on with Proxyclick, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2f343-147">**To configure Azure AD single sign-on with Proxyclick, perform the following steps:**</span></span>

1. <span data-ttu-id="2f343-148">In the Azure portal, on the **Proxyclick** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2f343-148">In the Azure portal, on the **Proxyclick** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="2f343-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2f343-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/proxyclick-tutorial/tutorial_proxyclick_samlbase.png)

1. <span data-ttu-id="2f343-152">On the **Proxyclick Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="2f343-152">On the **Proxyclick Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Proxyclick Domain and URLs single sign-on information](./media/proxyclick-tutorial/tutorial_proxyclick_url2.png)

    <span data-ttu-id="2f343-154">a.</span><span class="sxs-lookup"><span data-stu-id="2f343-154">a.</span></span> <span data-ttu-id="2f343-155">In the **Identifier** textbox, type a URL using the following pattern: `https://saml.proxyclick.com/init/<companyId>`</span><span class="sxs-lookup"><span data-stu-id="2f343-155">In the **Identifier** textbox, type a URL using the following pattern: `https://saml.proxyclick.com/init/<companyId>`</span></span>

    <span data-ttu-id="2f343-156">b.</span><span class="sxs-lookup"><span data-stu-id="2f343-156">b.</span></span> <span data-ttu-id="2f343-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://saml.proxyclick.com/consume/<companyId>`</span><span class="sxs-lookup"><span data-stu-id="2f343-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://saml.proxyclick.com/consume/<companyId>`</span></span>

1. <span data-ttu-id="2f343-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="2f343-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Proxyclick Domain and URLs single sign-on information](./media/proxyclick-tutorial/tutorial_proxyclick_url1.png)

    <span data-ttu-id="2f343-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://saml.proxyclick.com/init/<companyId>`</span><span class="sxs-lookup"><span data-stu-id="2f343-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://saml.proxyclick.com/init/<companyId>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="2f343-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="2f343-161">These values are not real.</span></span> <span data-ttu-id="2f343-162">You will update these values with the actual Identifier, Reply URL, and Sign-On URL, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="2f343-162">You will update these values with the actual Identifier, Reply URL, and Sign-On URL, which is explained later in the tutorial.</span></span>

1. <span data-ttu-id="2f343-163">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="2f343-163">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/proxyclick-tutorial/tutorial_proxyclick_certificate.png) 

1. <span data-ttu-id="2f343-165">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="2f343-165">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/proxyclick-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="2f343-167">On the **Proxyclick Configuration** section, click **Configure Proxyclick** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="2f343-167">On the **Proxyclick Configuration** section, click **Configure Proxyclick** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2f343-168">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="2f343-168">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Proxyclick Configuration](./media/proxyclick-tutorial/tutorial_proxyclick_configure.png)

1. <span data-ttu-id="2f343-170">In a different web browser window, log in to your Proxyclick company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="2f343-170">In a different web browser window, log in to your Proxyclick company site as an administrator.</span></span>

1. <span data-ttu-id="2f343-171">Select **Account & Settings**.</span><span class="sxs-lookup"><span data-stu-id="2f343-171">Select **Account & Settings**.</span></span>

    ![Proxyclick Configuration](./media/proxyclick-tutorial/configure1.png)

1. <span data-ttu-id="2f343-173">Scroll down to the **INTEGRATIONS** and select **SAML**.</span><span class="sxs-lookup"><span data-stu-id="2f343-173">Scroll down to the **INTEGRATIONS** and select **SAML**.</span></span>

    ![Proxyclick Configuration](./media/proxyclick-tutorial/configure2.png)

1. <span data-ttu-id="2f343-175">In the **SAML** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2f343-175">In the **SAML** section, perform the following steps:</span></span>

    ![Proxyclick Configuration](./media/proxyclick-tutorial/configure3.png)

    <span data-ttu-id="2f343-177">a.</span><span class="sxs-lookup"><span data-stu-id="2f343-177">a.</span></span> <span data-ttu-id="2f343-178">Copy **SAML Consumer URL** value and paste it into **Reply URL** textbox in **Proxyclick Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2f343-178">Copy **SAML Consumer URL** value and paste it into **Reply URL** textbox in **Proxyclick Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="2f343-179">b.</span><span class="sxs-lookup"><span data-stu-id="2f343-179">b.</span></span> <span data-ttu-id="2f343-180">Copy **SAML SSO Redirect URL** value and paste it into **Sign on URL** and **Identifier** textboxes in **Proxyclick Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2f343-180">Copy **SAML SSO Redirect URL** value and paste it into **Sign on URL** and **Identifier** textboxes in **Proxyclick Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="2f343-181">c.</span><span class="sxs-lookup"><span data-stu-id="2f343-181">c.</span></span> <span data-ttu-id="2f343-182">Select **SAML Request Method** as **HTTP Redirect**.</span><span class="sxs-lookup"><span data-stu-id="2f343-182">Select **SAML Request Method** as **HTTP Redirect**.</span></span>

    <span data-ttu-id="2f343-183">d.</span><span class="sxs-lookup"><span data-stu-id="2f343-183">d.</span></span> <span data-ttu-id="2f343-184">In the **Issuer** textbox, paste the value of **SAML Entity ID** value, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2f343-184">In the **Issuer** textbox, paste the value of **SAML Entity ID** value, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2f343-185">e.</span><span class="sxs-lookup"><span data-stu-id="2f343-185">e.</span></span> <span data-ttu-id="2f343-186">In the **SAML 2.0 Endpoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2f343-186">In the **SAML 2.0 Endpoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    <span data-ttu-id="2f343-187">f.</span><span class="sxs-lookup"><span data-stu-id="2f343-187">f.</span></span> <span data-ttu-id="2f343-188">Open your downloaded certificate file from Azure portal in Notepad and then paste it into the **Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="2f343-188">Open your downloaded certificate file from Azure portal in Notepad and then paste it into the **Certificate** textbox.</span></span>

    <span data-ttu-id="2f343-189">g.</span><span class="sxs-lookup"><span data-stu-id="2f343-189">g.</span></span> <span data-ttu-id="2f343-190">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="2f343-190">Click **Save Changes**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2f343-191">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2f343-191">Create an Azure AD test user</span></span>

<span data-ttu-id="2f343-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2f343-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="2f343-194">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2f343-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2f343-195">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="2f343-195">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/proxyclick-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="2f343-197">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="2f343-197">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/proxyclick-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="2f343-199">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="2f343-199">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/proxyclick-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="2f343-201">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2f343-201">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/proxyclick-tutorial/create_aaduser_04.png)

    <span data-ttu-id="2f343-203">a.</span><span class="sxs-lookup"><span data-stu-id="2f343-203">a.</span></span> <span data-ttu-id="2f343-204">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2f343-204">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2f343-205">b.</span><span class="sxs-lookup"><span data-stu-id="2f343-205">b.</span></span> <span data-ttu-id="2f343-206">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2f343-206">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="2f343-207">c.</span><span class="sxs-lookup"><span data-stu-id="2f343-207">c.</span></span> <span data-ttu-id="2f343-208">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="2f343-208">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="2f343-209">d.</span><span class="sxs-lookup"><span data-stu-id="2f343-209">d.</span></span> <span data-ttu-id="2f343-210">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="2f343-210">Click **Create**.</span></span>

### <a name="create-a-proxyclick-test-user"></a><span data-ttu-id="2f343-211">Create a Proxyclick test user</span><span class="sxs-lookup"><span data-stu-id="2f343-211">Create a Proxyclick test user</span></span>

<span data-ttu-id="2f343-212">To enable Azure AD users to log in to Proxyclick, they must be provisioned into Proxyclick.</span><span class="sxs-lookup"><span data-stu-id="2f343-212">To enable Azure AD users to log in to Proxyclick, they must be provisioned into Proxyclick.</span></span> <span data-ttu-id="2f343-213">In the case of Proxyclick, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="2f343-213">In the case of Proxyclick, provisioning is a manual task.</span></span>

<span data-ttu-id="2f343-214">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2f343-214">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="2f343-215">Log in to your Proxyclick company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="2f343-215">Log in to your Proxyclick company site as an administrator.</span></span>

1. <span data-ttu-id="2f343-216">Click **Colleagues** from the top navigation bar.</span><span class="sxs-lookup"><span data-stu-id="2f343-216">Click **Colleagues** from the top navigation bar.</span></span>

    ![Add Employee](./media/proxyclick-tutorial/user1.png)

1. <span data-ttu-id="2f343-218">Click **Add Colleague**</span><span class="sxs-lookup"><span data-stu-id="2f343-218">Click **Add Colleague**</span></span>

    ![Add Employee](./media/proxyclick-tutorial/user2.png)

1. <span data-ttu-id="2f343-220">In the **Add a colleague** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2f343-220">In the **Add a colleague** section, perform the following steps:</span></span>

    ![Add Employee](./media/proxyclick-tutorial/user3.png)

    <span data-ttu-id="2f343-222">a.</span><span class="sxs-lookup"><span data-stu-id="2f343-222">a.</span></span> <span data-ttu-id="2f343-223">In the **Email** textbox, type the email address of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="2f343-223">In the **Email** textbox, type the email address of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="2f343-224">b.</span><span class="sxs-lookup"><span data-stu-id="2f343-224">b.</span></span> <span data-ttu-id="2f343-225">In the **First Name** textbox, type the first name of user like Britta.</span><span class="sxs-lookup"><span data-stu-id="2f343-225">In the **First Name** textbox, type the first name of user like Britta.</span></span>

    <span data-ttu-id="2f343-226">c.</span><span class="sxs-lookup"><span data-stu-id="2f343-226">c.</span></span> <span data-ttu-id="2f343-227">In the **Last Name** textbox, type the last name of user like Simon.</span><span class="sxs-lookup"><span data-stu-id="2f343-227">In the **Last Name** textbox, type the last name of user like Simon.</span></span>

    <span data-ttu-id="2f343-228">d.</span><span class="sxs-lookup"><span data-stu-id="2f343-228">d.</span></span> <span data-ttu-id="2f343-229">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="2f343-229">Click **Add User**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="2f343-230">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2f343-230">Assign the Azure AD test user</span></span>

<span data-ttu-id="2f343-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Proxyclick.</span><span class="sxs-lookup"><span data-stu-id="2f343-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Proxyclick.</span></span>

![Assign the user role][200]

<span data-ttu-id="2f343-233">**To assign Britta Simon to Proxyclick, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2f343-233">**To assign Britta Simon to Proxyclick, perform the following steps:**</span></span>

1. <span data-ttu-id="2f343-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2f343-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="2f343-236">In the applications list, select **Proxyclick**.</span><span class="sxs-lookup"><span data-stu-id="2f343-236">In the applications list, select **Proxyclick**.</span></span>

    ![The Proxyclick link in the Applications list](./media/proxyclick-tutorial/tutorial_proxyclick_app.png)  

1. <span data-ttu-id="2f343-238">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="2f343-238">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="2f343-240">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="2f343-240">Click **Add** button.</span></span> <span data-ttu-id="2f343-241">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2f343-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="2f343-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="2f343-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="2f343-244">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="2f343-244">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="2f343-245">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2f343-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2f343-246">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="2f343-246">Test single sign-on</span></span>

<span data-ttu-id="2f343-247">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="2f343-247">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2f343-248">When you click the Proxyclick tile in the Access Panel, you should get automatically signed-on to your Proxyclick application.</span><span class="sxs-lookup"><span data-stu-id="2f343-248">When you click the Proxyclick tile in the Access Panel, you should get automatically signed-on to your Proxyclick application.</span></span>
<span data-ttu-id="2f343-249">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2f343-249">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2f343-250">Additional resources</span><span class="sxs-lookup"><span data-stu-id="2f343-250">Additional resources</span></span>

* [<span data-ttu-id="2f343-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f343-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="2f343-252">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2f343-252">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/proxyclick-tutorial/tutorial_general_01.png
[2]: ./media/proxyclick-tutorial/tutorial_general_02.png
[3]: ./media/proxyclick-tutorial/tutorial_general_03.png
[4]: ./media/proxyclick-tutorial/tutorial_general_04.png

[100]: ./media/proxyclick-tutorial/tutorial_general_100.png

[200]: ./media/proxyclick-tutorial/tutorial_general_200.png
[201]: ./media/proxyclick-tutorial/tutorial_general_201.png
[202]: ./media/proxyclick-tutorial/tutorial_general_202.png
[203]: ./media/proxyclick-tutorial/tutorial_general_203.png

