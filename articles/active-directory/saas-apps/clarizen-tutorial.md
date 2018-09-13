---
title: 'Tutorial: Azure Active Directory integration with Clarizen | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Clarizen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: jeedes
ms.openlocfilehash: 855f147b0622ecc0831f2bc464e83d245af9e574
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870946"
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="dd9dc-103">Tutorial: Azure Active Directory integration with Clarizen</span><span class="sxs-lookup"><span data-stu-id="dd9dc-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="dd9dc-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with Clarizen.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="dd9dc-105">This integration gives you the following benefits:</span><span class="sxs-lookup"><span data-stu-id="dd9dc-105">This integration gives you the following benefits:</span></span>

- <span data-ttu-id="dd9dc-106">You can control, in Azure AD, who has access to Clarizen.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-106">You can control, in Azure AD, who has access to Clarizen.</span></span>
- <span data-ttu-id="dd9dc-107">You can enable your users to be automatically signed in to Clarizen (single sign-on) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-107">You can enable your users to be automatically signed in to Clarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="dd9dc-108">You can manage your accounts in one central location, the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-108">You can manage your accounts in one central location, the Azure portal.</span></span>

<span data-ttu-id="dd9dc-109">The scenario in this tutorial consists of two main tasks:</span><span class="sxs-lookup"><span data-stu-id="dd9dc-109">The scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="dd9dc-110">Add Clarizen from the gallery.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-110">Add Clarizen from the gallery.</span></span>
1. <span data-ttu-id="dd9dc-111">Configure and test Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="dd9dc-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="dd9dc-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd9dc-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dd9dc-113">Prerequisites</span></span>
<span data-ttu-id="dd9dc-114">To configure Azure AD integration with Clarizen, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="dd9dc-114">To configure Azure AD integration with Clarizen, you need the following items:</span></span>

- <span data-ttu-id="dd9dc-115">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="dd9dc-115">An Azure AD subscription</span></span>
- <span data-ttu-id="dd9dc-116">A Clarizen subscription that's enabled for single sign-on</span><span class="sxs-lookup"><span data-stu-id="dd9dc-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="dd9dc-117">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="dd9dc-117">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="dd9dc-118">Test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dd9dc-119">Don't use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="dd9dc-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dd9dc-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-the-gallery"></a><span data-ttu-id="dd9dc-121">Add Clarizen from the gallery</span><span class="sxs-lookup"><span data-stu-id="dd9dc-121">Add Clarizen from the gallery</span></span>
<span data-ttu-id="dd9dc-122">To configure the integration of Clarizen into Azure AD, add Clarizen from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-122">To configure the integration of Clarizen into Azure AD, add Clarizen from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="dd9dc-123">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-123">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory icon][1]

1. <span data-ttu-id="dd9dc-125">Click **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="dd9dc-126">Then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-126">Then click **All applications**.</span></span>

    ![Clicking "Enterprise applications" and "All applications"][2]

1. <span data-ttu-id="dd9dc-128">Click the **Add** button at the top of the dialog box.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-128">Click the **Add** button at the top of the dialog box.</span></span>

    ![The "Add" button][3]

1. <span data-ttu-id="dd9dc-130">In the search box, type **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-130">In the search box, type **Clarizen**.</span></span>

    ![Typing "Clarizen" in the search box](./media/clarizen-tutorial/tutorial_clarizen_000.png)

1. <span data-ttu-id="dd9dc-132">In the results pane, select **Clarizen**, and then click **Add** to add the application.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-132">In the results pane, select **Clarizen**, and then click **Add** to add the application.</span></span>

    ![Selecting Clarizen in the results pane](./media/clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="dd9dc-134">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dd9dc-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="dd9dc-135">In the following sections, you configure and test Azure AD single sign-on with Clarizen based on the test user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-135">In the following sections, you configure and test Azure AD single sign-on with Clarizen based on the test user Britta Simon.</span></span>

<span data-ttu-id="dd9dc-136">For single sign-on to work, Azure AD needs to know what the counterpart user in Clarizen is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-136">For single sign-on to work, Azure AD needs to know what the counterpart user in Clarizen is to a user in Azure AD.</span></span> <span data-ttu-id="dd9dc-137">In other words, a link relationship between an Azure AD user and the related user in Clarizen needs to be established.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-137">In other words, a link relationship between an Azure AD user and the related user in Clarizen needs to be established.</span></span> <span data-ttu-id="dd9dc-138">You establish this link relationship by assigning the value of **user name** in Azure AD as the value of **Username** in Clarizen.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-138">You establish this link relationship by assigning the value of **user name** in Azure AD as the value of **Username** in Clarizen.</span></span>

<span data-ttu-id="dd9dc-139">To configure and test Azure AD single sign-on with Clarizen, complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="dd9dc-139">To configure and test Azure AD single sign-on with Clarizen, complete the following building blocks:</span></span>

1. <span data-ttu-id="dd9dc-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** to enable your users to use this feature.</span></span>
1. <span data-ttu-id="dd9dc-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="dd9dc-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** to have a counterpart of Britta Simon in Clarizen that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** to have a counterpart of Britta Simon in Clarizen that is linked to the Azure AD representation of her.</span></span>
1. <span data-ttu-id="dd9dc-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="dd9dc-144">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-144">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="dd9dc-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dd9dc-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="dd9dc-146">Enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clarizen application.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-146">Enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="dd9dc-147">In the Azure portal, on the **Clarizen** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-147">In the Azure portal, on the **Clarizen** application integration page, click **Single sign-on**.</span></span>

    ![Clicking "Single sign-on"][4]

1. <span data-ttu-id="dd9dc-149">In the **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-149">In the **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Selecting "SAML-based Sign-on"](./media/clarizen-tutorial/tutorial_clarizen_01.png)

1. <span data-ttu-id="dd9dc-151">In the **Clarizen Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dd9dc-151">In the **Clarizen Domain and URLs** section, perform the following steps:</span></span>

    ![Boxes for identifier and reply URL](./media/clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="dd9dc-153">a.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-153">a.</span></span> <span data-ttu-id="dd9dc-154">In the **Identifier** box, type the value as: **Clarizen**</span><span class="sxs-lookup"><span data-stu-id="dd9dc-154">In the **Identifier** box, type the value as: **Clarizen**</span></span>

    <span data-ttu-id="dd9dc-155">b.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-155">b.</span></span> <span data-ttu-id="dd9dc-156">In the **Reply URL** box, type a URL by using the following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="dd9dc-156">In the **Reply URL** box, type a URL by using the following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="dd9dc-157">These are not the real values.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-157">These are not the real values.</span></span> <span data-ttu-id="dd9dc-158">You have to use the actual identifier and reply URL.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-158">You have to use the actual identifier and reply URL.</span></span> <span data-ttu-id="dd9dc-159">Here we suggest that you use the unique value of a string as the identifier.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-159">Here we suggest that you use the unique value of a string as the identifier.</span></span> <span data-ttu-id="dd9dc-160">To get the actual values, contact the [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span><span class="sxs-lookup"><span data-stu-id="dd9dc-160">To get the actual values, contact the [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

1. <span data-ttu-id="dd9dc-161">On the **SAML Signing Certificate** section, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-161">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Clicking "Create new certificate"](./media/clarizen-tutorial/tutorial_clarizen_03.png)    

1. <span data-ttu-id="dd9dc-163">In the **Create New Certificate** dialog box, click the calendar icon and select an expiry date.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-163">In the **Create New Certificate** dialog box, click the calendar icon and select an expiry date.</span></span> <span data-ttu-id="dd9dc-164">Then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-164">Then click **Save**.</span></span>

    ![Selecting and saving an expiry date](./media/clarizen-tutorial/tutorial_general_300.png)

1. <span data-ttu-id="dd9dc-166">In the **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-166">In the **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![Selecting the check box for making the new certificate active](./media/clarizen-tutorial/tutorial_clarizen_04.png)

1. <span data-ttu-id="dd9dc-168">In the **Rollover certificate** dialog box, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-168">In the **Rollover certificate** dialog box, click **OK**.</span></span>

    ![Clicking "OK" to confirm that you want to make the certificate active](./media/clarizen-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="dd9dc-170">In the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-170">In the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Clicking "Certificate (Base64)" to start the download](./media/clarizen-tutorial/tutorial_clarizen_05.png)

1. <span data-ttu-id="dd9dc-172">In the **Clarizen Configuration** section, click **Configure Clarizen** to open the **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-172">In the **Clarizen Configuration** section, click **Configure Clarizen** to open the **Configure sign-on** window.</span></span>

    ![Clicking "Configure Clarizen"](./media/clarizen-tutorial/tutorial_clarizen_06.png)

    !["Configure sign-on" window, including files and URLs](./media/clarizen-tutorial/tutorial_clarizen_07.png)

1. <span data-ttu-id="dd9dc-175">In a different web browser window, sign in to your Clarizen company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-175">In a different web browser window, sign in to your Clarizen company site as an administrator.</span></span>

1. <span data-ttu-id="dd9dc-176">Click your username, and then click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="dd9dc-177">![Clicking "Settings" under your username](./media/clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="dd9dc-177">![Clicking "Settings" under your username](./media/clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

1. <span data-ttu-id="dd9dc-178">Click the **Global Settings** tab. Then, next to **Federated Authentication**, click **edit**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-178">Click the **Global Settings** tab. Then, next to **Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="dd9dc-179">!["Global Settings" tab](./media/clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span><span class="sxs-lookup"><span data-stu-id="dd9dc-179">!["Global Settings" tab](./media/clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

1. <span data-ttu-id="dd9dc-180">In the **Federated Authentication** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dd9dc-180">In the **Federated Authentication** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="dd9dc-181">!["Federated Authentication" dialog box](./media/clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span><span class="sxs-lookup"><span data-stu-id="dd9dc-181">!["Federated Authentication" dialog box](./media/clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="dd9dc-182">a.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-182">a.</span></span> <span data-ttu-id="dd9dc-183">Select **Enable Federated Authentication**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-183">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="dd9dc-184">b.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-184">b.</span></span> <span data-ttu-id="dd9dc-185">Click **Upload** to upload your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-185">Click **Upload** to upload your downloaded certificate.</span></span>

    <span data-ttu-id="dd9dc-186">c.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-186">c.</span></span> <span data-ttu-id="dd9dc-187">In the **Sign-in URL** box, enter the value of **SAML Single Sign-On Service URL** from the Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-187">In the **Sign-in URL** box, enter the value of **SAML Single Sign-On Service URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="dd9dc-188">d.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-188">d.</span></span> <span data-ttu-id="dd9dc-189">In the **Sign-out URL** box, enter the value of **Sign-Out URL** from the Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-189">In the **Sign-out URL** box, enter the value of **Sign-Out URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="dd9dc-190">e.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-190">e.</span></span> <span data-ttu-id="dd9dc-191">Select **Use POST**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-191">Select **Use POST**.</span></span>

    <span data-ttu-id="dd9dc-192">f.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-192">f.</span></span> <span data-ttu-id="dd9dc-193">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-193">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="dd9dc-194">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="dd9dc-194">Create an Azure AD test user</span></span>
<span data-ttu-id="dd9dc-195">In the Azure portal, create a test user called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-195">In the Azure portal, create a test user called Britta Simon.</span></span>

![Name and email address of the Azure AD test user][100]

1. <span data-ttu-id="dd9dc-197">In the Azure portal, in the left pane, click the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-197">In the Azure portal, in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory icon](./media/clarizen-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="dd9dc-199">Click **Users and groups**, and then click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-199">Click **Users and groups**, and then click **All users** to display the list of users.</span></span>

    ![Clicking "Users and groups" and "All users"](./media/clarizen-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="dd9dc-201">At the top of the dialog box, click **Add** to open the **User** dialog box.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-201">At the top of the dialog box, click **Add** to open the **User** dialog box.</span></span>

    ![The "Add" button](./media/clarizen-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="dd9dc-203">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dd9dc-203">In the **User** dialog box, perform the following steps:</span></span>

    !["User" dialog box with name, email address, and password filled in](./media/clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="dd9dc-205">a.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-205">a.</span></span> <span data-ttu-id="dd9dc-206">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-206">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dd9dc-207">b.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-207">b.</span></span> <span data-ttu-id="dd9dc-208">In the **User name** box, type the email address of the Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-208">In the **User name** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="dd9dc-209">c.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-209">c.</span></span> <span data-ttu-id="dd9dc-210">Select **Show Password** and write down the value of **Password**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-210">Select **Show Password** and write down the value of **Password**.</span></span>

    <span data-ttu-id="dd9dc-211">d.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-211">d.</span></span> <span data-ttu-id="dd9dc-212">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-212">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="dd9dc-213">Create a Clarizen test user</span><span class="sxs-lookup"><span data-stu-id="dd9dc-213">Create a Clarizen test user</span></span>

<span data-ttu-id="dd9dc-214">The objective of this section is to create a user called Britta Simon in Clarizen.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-214">The objective of this section is to create a user called Britta Simon in Clarizen.</span></span>

<span data-ttu-id="dd9dc-215">**If you need to create user manually, please perform following steps:**</span><span class="sxs-lookup"><span data-stu-id="dd9dc-215">**If you need to create user manually, please perform following steps:**</span></span>

<span data-ttu-id="dd9dc-216">To enable Azure AD users to sign in to Clarizen, you must provision user accounts.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-216">To enable Azure AD users to sign in to Clarizen, you must provision user accounts.</span></span> <span data-ttu-id="dd9dc-217">In the case of Clarizen, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-217">In the case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="dd9dc-218">Sign in to your Clarizen company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-218">Sign in to your Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="dd9dc-219">Click **People**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-219">Click **People**.</span></span>

    <span data-ttu-id="dd9dc-220">![Clicking "People"](./media/clarizen-tutorial/create_aaduser_001.png "People")</span><span class="sxs-lookup"><span data-stu-id="dd9dc-220">![Clicking "People"](./media/clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="dd9dc-221">Click **Invite User**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-221">Click **Invite User**.</span></span>

    <span data-ttu-id="dd9dc-222">!["Invite User" button](./media/clarizen-tutorial/create_aaduser_002.png "Invite Users")</span><span class="sxs-lookup"><span data-stu-id="dd9dc-222">!["Invite User" button](./media/clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

1. <span data-ttu-id="dd9dc-223">In the **Invite People** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dd9dc-223">In the **Invite People** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="dd9dc-224">!["Invite People" dialog box](./media/clarizen-tutorial/create_aaduser_003.png "Invite People")</span><span class="sxs-lookup"><span data-stu-id="dd9dc-224">!["Invite People" dialog box](./media/clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="dd9dc-225">a.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-225">a.</span></span> <span data-ttu-id="dd9dc-226">In the **Email** box, type the email address of the Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-226">In the **Email** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="dd9dc-227">b.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-227">b.</span></span> <span data-ttu-id="dd9dc-228">Click **Invite**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-228">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dd9dc-229">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-229">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="dd9dc-230">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="dd9dc-230">Assign the Azure AD test user</span></span>
<span data-ttu-id="dd9dc-231">Enable Britta Simon to use Azure single sign-on by granting her access to Clarizen.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-231">Enable Britta Simon to use Azure single sign-on by granting her access to Clarizen.</span></span>

![Assigned test user][200]

1. <span data-ttu-id="dd9dc-233">In the Azure portal, open the applications view, browse to the directory view, click **Enterprise applications**, and then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-233">In the Azure portal, open the applications view, browse to the directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![Clicking "Enterprise applications" and "All applications"][201]

1. <span data-ttu-id="dd9dc-235">In the applications list, select **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-235">In the applications list, select **Clarizen**.</span></span>

    ![Selecting Clarizen in the list](./media/clarizen-tutorial/tutorial_clarizen_50.png)

1. <span data-ttu-id="dd9dc-237">In the left pane, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-237">In the left pane, click **Users and groups**.</span></span>

    ![Clicking "Users and groups"][202]

1. <span data-ttu-id="dd9dc-239">Click the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-239">Click the **Add** button.</span></span> <span data-ttu-id="dd9dc-240">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-240">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![The "Add" button and the "Add Assignment" dialog box][203]

1. <span data-ttu-id="dd9dc-242">In the **Users and groups** dialog box, select **Britta Simon** in the list of users.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-242">In the **Users and groups** dialog box, select **Britta Simon** in the list of users.</span></span>

1. <span data-ttu-id="dd9dc-243">In the **Users and groups** dialog box, click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-243">In the **Users and groups** dialog box, click the **Select** button.</span></span>

1. <span data-ttu-id="dd9dc-244">In the **Add Assignment** dialog box, click the **Assign** button.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-244">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="dd9dc-245">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="dd9dc-245">Test single sign-on</span></span>
<span data-ttu-id="dd9dc-246">Test your Azure AD single sign-on configuration by using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-246">Test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="dd9dc-247">When you click the Clarizen tile in the Access Panel, you should be automatically signed in to your Clarizen application.</span><span class="sxs-lookup"><span data-stu-id="dd9dc-247">When you click the Clarizen tile in the Access Panel, you should be automatically signed in to your Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dd9dc-248">Additional resources</span><span class="sxs-lookup"><span data-stu-id="dd9dc-248">Additional resources</span></span>

* [<span data-ttu-id="dd9dc-249">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd9dc-249">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="dd9dc-250">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dd9dc-250">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/clarizen-tutorial/tutorial_general_01.png
[2]: ./media/clarizen-tutorial/tutorial_general_02.png
[3]: ./media/clarizen-tutorial/tutorial_general_03.png
[4]: ./media/clarizen-tutorial/tutorial_general_04.png

[100]: ./media/clarizen-tutorial/tutorial_general_100.png

[200]: ./media/clarizen-tutorial/tutorial_general_200.png
[201]: ./media/clarizen-tutorial/tutorial_general_201.png
[202]: ./media/clarizen-tutorial/tutorial_general_202.png
[203]: ./media/clarizen-tutorial/tutorial_general_203.png