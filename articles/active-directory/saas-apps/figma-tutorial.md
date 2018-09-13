---
title: 'Tutorial: Azure Active Directory integration with Figma | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Figma.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8569cae1-87dd-4c40-9bbb-527ac80d6a96
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2018
ms.author: jeedes
ms.openlocfilehash: 4094de1a1c17e844d96ac789bb4bc1655fdc1546
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869416"
---
# <a name="tutorial-azure-active-directory-integration-with-figma"></a><span data-ttu-id="949f9-103">Tutorial: Azure Active Directory integration with Figma</span><span class="sxs-lookup"><span data-stu-id="949f9-103">Tutorial: Azure Active Directory integration with Figma</span></span>

<span data-ttu-id="949f9-104">In this tutorial, you learn how to integrate Figma with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="949f9-104">In this tutorial, you learn how to integrate Figma with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="949f9-105">Integrating Figma with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="949f9-105">Integrating Figma with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="949f9-106">You can control in Azure AD who has access to Figma.</span><span class="sxs-lookup"><span data-stu-id="949f9-106">You can control in Azure AD who has access to Figma.</span></span>
- <span data-ttu-id="949f9-107">You can enable your users to automatically get signed-on to Figma (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="949f9-107">You can enable your users to automatically get signed-on to Figma (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="949f9-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="949f9-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="949f9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span><span class="sxs-lookup"><span data-stu-id="949f9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="949f9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="949f9-110">Prerequisites</span></span>

<span data-ttu-id="949f9-111">To configure Azure AD integration with Figma, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="949f9-111">To configure Azure AD integration with Figma, you need the following items:</span></span>

- <span data-ttu-id="949f9-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="949f9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="949f9-113">A Figma [single sign-on enabled subscription](https://www.figma.com/pricing/)</span><span class="sxs-lookup"><span data-stu-id="949f9-113">A Figma [single sign-on enabled subscription](https://www.figma.com/pricing/)</span></span>

> [!NOTE]
> <span data-ttu-id="949f9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="949f9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> <span data-ttu-id="949f9-115">New customers and active subscribers of Figma Professional Team may contact Figma to [upgrade their subscription](https://www.figma.com/pricing/) to the Figma Organization Tier.</span><span class="sxs-lookup"><span data-stu-id="949f9-115">New customers and active subscribers of Figma Professional Team may contact Figma to [upgrade their subscription](https://www.figma.com/pricing/) to the Figma Organization Tier.</span></span>

<span data-ttu-id="949f9-116">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="949f9-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="949f9-117">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="949f9-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="949f9-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="949f9-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="949f9-119">Scenario description</span><span class="sxs-lookup"><span data-stu-id="949f9-119">Scenario description</span></span>

<span data-ttu-id="949f9-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="949f9-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="949f9-121">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="949f9-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="949f9-122">Adding Figma from the gallery</span><span class="sxs-lookup"><span data-stu-id="949f9-122">Adding Figma from the gallery</span></span>
2. <span data-ttu-id="949f9-123">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="949f9-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-figma-from-the-gallery"></a><span data-ttu-id="949f9-124">Adding Figma from the gallery</span><span class="sxs-lookup"><span data-stu-id="949f9-124">Adding Figma from the gallery</span></span>

<span data-ttu-id="949f9-125">To configure the integration of Figma into Azure AD, you need to add Figma from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="949f9-125">To configure the integration of Figma into Azure AD, you need to add Figma from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="949f9-126">**To add Figma from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="949f9-126">**To add Figma from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="949f9-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="949f9-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="949f9-129">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="949f9-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="949f9-130">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="949f9-130">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="949f9-132">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="949f9-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="949f9-134">In the search box, type **Figma**, select **Figma** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="949f9-134">In the search box, type **Figma**, select **Figma** from result panel then click **Add** button to add the application.</span></span>

    ![Figma in the results list](./media/figma-tutorial/tutorial_figma_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="949f9-136">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="949f9-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="949f9-137">In this section, you configure and test Azure AD single sign-on with Figma based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="949f9-137">In this section, you configure and test Azure AD single sign-on with Figma based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="949f9-138">For single sign-on to work, Azure AD needs to be linked to Figma.</span><span class="sxs-lookup"><span data-stu-id="949f9-138">For single sign-on to work, Azure AD needs to be linked to Figma.</span></span>  <span data-ttu-id="949f9-139">To configure and test Azure AD single sign-on with Figma, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="949f9-139">To configure and test Azure AD single sign-on with Figma, complete the following steps:</span></span>

1. <span data-ttu-id="949f9-140">[**Contact Figma support team**](mailto:support@figma.com?subject=SAML+Config) to initiate a SAML configuration for your organization and get an ORG_SAML_CONFIG_ID.</span><span class="sxs-lookup"><span data-stu-id="949f9-140">[**Contact Figma support team**](mailto:support@figma.com?subject=SAML+Config) to initiate a SAML configuration for your organization and get an ORG_SAML_CONFIG_ID.</span></span>
2. <span data-ttu-id="949f9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="949f9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
3. <span data-ttu-id="949f9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="949f9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="949f9-143">**[Create a Figma test user](#create-a-figma-test-user)** - to have a counterpart of Britta Simon in Figma that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="949f9-143">**[Create a Figma test user](#create-a-figma-test-user)** - to have a counterpart of Britta Simon in Figma that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="949f9-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="949f9-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="949f9-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="949f9-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="949f9-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="949f9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="949f9-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Figma application.</span><span class="sxs-lookup"><span data-stu-id="949f9-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Figma application.</span></span>

<span data-ttu-id="949f9-148">**To configure Azure AD single sign-on with Figma, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="949f9-148">**To configure Azure AD single sign-on with Figma, perform the following steps:**</span></span>

1. <span data-ttu-id="949f9-149">In the Azure portal, on the **Figma** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="949f9-149">In the Azure portal, on the **Figma** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="949f9-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="949f9-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/figma-tutorial/tutorial_figma_samlbase.png)

3. <span data-ttu-id="949f9-153">On the **Figma Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="949f9-153">On the **Figma Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Figma Domain and URLs single sign-on information](./media/figma-tutorial/tutorial_figma_url1.png)

    <span data-ttu-id="949f9-155">a.</span><span class="sxs-lookup"><span data-stu-id="949f9-155">a.</span></span> <span data-ttu-id="949f9-156">In the **Identifier** textbox, type a URL using the following pattern: `https://www.figma.com/saml/<ORG_SAML_CONFIG_ID>`</span><span class="sxs-lookup"><span data-stu-id="949f9-156">In the **Identifier** textbox, type a URL using the following pattern: `https://www.figma.com/saml/<ORG_SAML_CONFIG_ID>`</span></span>

    <span data-ttu-id="949f9-157">b.</span><span class="sxs-lookup"><span data-stu-id="949f9-157">b.</span></span> <span data-ttu-id="949f9-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.figma.com/saml/<ORG_SAML_CONFIG_ID>/consume`</span><span class="sxs-lookup"><span data-stu-id="949f9-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.figma.com/saml/<ORG_SAML_CONFIG_ID>/consume`</span></span>

4. <span data-ttu-id="949f9-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="949f9-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Figma Domain and URLs single sign-on information](./media/figma-tutorial/tutorial_figma_url2.png)

    <span data-ttu-id="949f9-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.figma.com/saml/<ORG_SAML_CONFIG_ID>/start`</span><span class="sxs-lookup"><span data-stu-id="949f9-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.figma.com/saml/<ORG_SAML_CONFIG_ID>/start`</span></span>

    > [!NOTE]
    > <span data-ttu-id="949f9-162">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="949f9-162">These values are not real.</span></span> <span data-ttu-id="949f9-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="949f9-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="949f9-164">Contact [Figma support team](mailto:support@figma.com?subject=SAML+Config) to get these values.</span><span class="sxs-lookup"><span data-stu-id="949f9-164">Contact [Figma support team](mailto:support@figma.com?subject=SAML+Config) to get these values.</span></span>

5. <span data-ttu-id="949f9-165">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="949f9-165">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

    ![The Certificate download link](./media/figma-tutorial/tutorial_figma_certificate.png)

6. <span data-ttu-id="949f9-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="949f9-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/figma-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="949f9-169">To configure single sign-on on Figma side, please fill out this form: [https://goo.gl/forms/XkRB1z5ed4eVUzXn2](https://goo.gl/forms/XkRB1z5ed4eVUzXn2).</span><span class="sxs-lookup"><span data-stu-id="949f9-169">To configure single sign-on on Figma side, please fill out this form: [https://goo.gl/forms/XkRB1z5ed4eVUzXn2](https://goo.gl/forms/XkRB1z5ed4eVUzXn2).</span></span> <span data-ttu-id="949f9-170">It will accept your **App Federation Metadata Url** from Step #5.</span><span class="sxs-lookup"><span data-stu-id="949f9-170">It will accept your **App Federation Metadata Url** from Step #5.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="949f9-171">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="949f9-171">Create an Azure AD test user</span></span>

<span data-ttu-id="949f9-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="949f9-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="949f9-174">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="949f9-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="949f9-175">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="949f9-175">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/figma-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="949f9-177">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="949f9-177">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/figma-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="949f9-179">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="949f9-179">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/figma-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="949f9-181">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="949f9-181">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/figma-tutorial/create_aaduser_04.png)

    <span data-ttu-id="949f9-183">a.</span><span class="sxs-lookup"><span data-stu-id="949f9-183">a.</span></span> <span data-ttu-id="949f9-184">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="949f9-184">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="949f9-185">b.</span><span class="sxs-lookup"><span data-stu-id="949f9-185">b.</span></span> <span data-ttu-id="949f9-186">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="949f9-186">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="949f9-187">c.</span><span class="sxs-lookup"><span data-stu-id="949f9-187">c.</span></span> <span data-ttu-id="949f9-188">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="949f9-188">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="949f9-189">d.</span><span class="sxs-lookup"><span data-stu-id="949f9-189">d.</span></span> <span data-ttu-id="949f9-190">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="949f9-190">Click **Create**.</span></span>

### <a name="create-a-figma-test-user"></a><span data-ttu-id="949f9-191">Create a Figma test user</span><span class="sxs-lookup"><span data-stu-id="949f9-191">Create a Figma test user</span></span>

<span data-ttu-id="949f9-192">The objective of this section is to create a user called Britta Simon in Figma.</span><span class="sxs-lookup"><span data-stu-id="949f9-192">The objective of this section is to create a user called Britta Simon in Figma.</span></span> <span data-ttu-id="949f9-193">Figma supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="949f9-193">Figma supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="949f9-194">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="949f9-194">There is no action item for you in this section.</span></span> <span data-ttu-id="949f9-195">A new user is created during an attempt to access Figma if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="949f9-195">A new user is created during an attempt to access Figma if it doesn't exist yet.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="949f9-196">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="949f9-196">Assign the Azure AD test user</span></span>

<span data-ttu-id="949f9-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Figma.</span><span class="sxs-lookup"><span data-stu-id="949f9-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Figma.</span></span>

![Assign the user role][200]

<span data-ttu-id="949f9-199">**To assign Britta Simon to Figma, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="949f9-199">**To assign Britta Simon to Figma, perform the following steps:**</span></span>

1. <span data-ttu-id="949f9-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="949f9-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="949f9-202">In the applications list, select **Figma**.</span><span class="sxs-lookup"><span data-stu-id="949f9-202">In the applications list, select **Figma**.</span></span>

    ![The Figma link in the Applications list](./media/figma-tutorial/tutorial_figma_app.png)  

3. <span data-ttu-id="949f9-204">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="949f9-204">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="949f9-206">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="949f9-206">Click **Add** button.</span></span> <span data-ttu-id="949f9-207">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="949f9-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="949f9-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="949f9-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="949f9-210">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="949f9-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="949f9-211">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="949f9-211">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="949f9-212">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="949f9-212">Test single sign-on</span></span>

<span data-ttu-id="949f9-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="949f9-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="949f9-214">When you click the Figma tile in the Access Panel, you should get automatically signed-on to your Figma application.</span><span class="sxs-lookup"><span data-stu-id="949f9-214">When you click the Figma tile in the Access Panel, you should get automatically signed-on to your Figma application.</span></span>
<span data-ttu-id="949f9-215">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="949f9-215">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="949f9-216">Additional resources</span><span class="sxs-lookup"><span data-stu-id="949f9-216">Additional resources</span></span>

* [<span data-ttu-id="949f9-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="949f9-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="949f9-218">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="949f9-218">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/figma-tutorial/tutorial_general_01.png
[2]: ./media/figma-tutorial/tutorial_general_02.png
[3]: ./media/figma-tutorial/tutorial_general_03.png
[4]: ./media/figma-tutorial/tutorial_general_04.png

[100]: ./media/figma-tutorial/tutorial_general_100.png

[200]: ./media/figma-tutorial/tutorial_general_200.png
[201]: ./media/figma-tutorial/tutorial_general_201.png
[202]: ./media/figma-tutorial/tutorial_general_202.png
[203]: ./media/figma-tutorial/tutorial_general_203.png