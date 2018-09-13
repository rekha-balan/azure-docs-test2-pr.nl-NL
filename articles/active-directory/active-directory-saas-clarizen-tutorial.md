---
title: 'Tutorial: Azure Active Directory integration with Clarizen | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Clarizen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: bad426804693f8490600035555fde187f4124801
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549776"
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="3d656-103">Tutorial: Azure Active Directory integration with Clarizen</span><span class="sxs-lookup"><span data-stu-id="3d656-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="3d656-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with Clarizen.</span><span class="sxs-lookup"><span data-stu-id="3d656-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="3d656-105">This integration gives you the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3d656-105">This integration gives you the following benefits:</span></span>

- <span data-ttu-id="3d656-106">You can control, in Azure AD, who has access to Clarizen.</span><span class="sxs-lookup"><span data-stu-id="3d656-106">You can control, in Azure AD, who has access to Clarizen.</span></span>
- <span data-ttu-id="3d656-107">You can enable your users to be automatically signed in to Clarizen (single sign-on) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="3d656-107">You can enable your users to be automatically signed in to Clarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3d656-108">You can manage your accounts in one central location, the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3d656-108">You can manage your accounts in one central location, the Azure portal.</span></span>

<span data-ttu-id="3d656-109">The scenario in this tutorial consists of two main tasks:</span><span class="sxs-lookup"><span data-stu-id="3d656-109">The scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="3d656-110">Add Clarizen from the gallery.</span><span class="sxs-lookup"><span data-stu-id="3d656-110">Add Clarizen from the gallery.</span></span>
2. <span data-ttu-id="3d656-111">Configure and test Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3d656-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="3d656-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3d656-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d656-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3d656-113">Prerequisites</span></span>
<span data-ttu-id="3d656-114">To configure Azure AD integration with Clarizen, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="3d656-114">To configure Azure AD integration with Clarizen, you need the following items:</span></span>

- <span data-ttu-id="3d656-115">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="3d656-115">An Azure AD subscription</span></span>
- <span data-ttu-id="3d656-116">A Clarizen subscription that's enabled for single sign-on</span><span class="sxs-lookup"><span data-stu-id="3d656-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="3d656-117">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="3d656-117">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="3d656-118">Test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="3d656-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3d656-119">Don't use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="3d656-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="3d656-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3d656-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-the-gallery"></a><span data-ttu-id="3d656-121">Add Clarizen from the gallery</span><span class="sxs-lookup"><span data-stu-id="3d656-121">Add Clarizen from the gallery</span></span>
<span data-ttu-id="3d656-122">To configure the integration of Clarizen into Azure AD, add Clarizen from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="3d656-122">To configure the integration of Clarizen into Azure AD, add Clarizen from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="3d656-123">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="3d656-123">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory icon][1]

2. <span data-ttu-id="3d656-125">Click **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="3d656-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="3d656-126">Then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3d656-126">Then click **All applications**.</span></span>

    ![Clicking "Enterprise applications" and "All applications"][2]

3. <span data-ttu-id="3d656-128">Click the **Add** button at the top of the dialog box.</span><span class="sxs-lookup"><span data-stu-id="3d656-128">Click the **Add** button at the top of the dialog box.</span></span>

    ![The "Add" button][3]

4. <span data-ttu-id="3d656-130">In the search box, type **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="3d656-130">In the search box, type **Clarizen**.</span></span>

    ![Typing "Clarizen" in the search box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="3d656-132">In the results pane, select **Clarizen**, and then click **Add** to add the application.</span><span class="sxs-lookup"><span data-stu-id="3d656-132">In the results pane, select **Clarizen**, and then click **Add** to add the application.</span></span>

    ![Selecting Clarizen in the results pane](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3d656-134">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3d656-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="3d656-135">In the following sections, you configure and test Azure AD single sign-on with Clarizen based on the test user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d656-135">In the following sections, you configure and test Azure AD single sign-on with Clarizen based on the test user Britta Simon.</span></span>

<span data-ttu-id="3d656-136">For single sign-on to work, Azure AD needs to know what the counterpart user in Clarizen is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d656-136">For single sign-on to work, Azure AD needs to know what the counterpart user in Clarizen is to a user in Azure AD.</span></span> <span data-ttu-id="3d656-137">In other words, a link relationship between an Azure AD user and the related user in Clarizen needs to be established.</span><span class="sxs-lookup"><span data-stu-id="3d656-137">In other words, a link relationship between an Azure AD user and the related user in Clarizen needs to be established.</span></span> <span data-ttu-id="3d656-138">You establish this link relationship by assigning the value of **user name** in Azure AD as the value of **Username** in Clarizen.</span><span class="sxs-lookup"><span data-stu-id="3d656-138">You establish this link relationship by assigning the value of **user name** in Azure AD as the value of **Username** in Clarizen.</span></span>

<span data-ttu-id="3d656-139">To configure and test Azure AD single sign-on with Clarizen, complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="3d656-139">To configure and test Azure AD single sign-on with Clarizen, complete the following building blocks:</span></span>

1. <span data-ttu-id="3d656-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="3d656-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3d656-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d656-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3d656-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** to have a counterpart of Britta Simon in Clarizen that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="3d656-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** to have a counterpart of Britta Simon in Clarizen that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="3d656-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3d656-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3d656-144">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="3d656-144">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3d656-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3d656-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="3d656-146">Enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clarizen application.</span><span class="sxs-lookup"><span data-stu-id="3d656-146">Enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="3d656-147">In the Azure portal, on the **Clarizen** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3d656-147">In the Azure portal, on the **Clarizen** application integration page, click **Single sign-on**.</span></span>

    ![Clicking "Single sign-on"][4]

2. <span data-ttu-id="3d656-149">In the **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3d656-149">In the **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Selecting "SAML-based Sign-on"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="3d656-151">In the **Clarizen Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3d656-151">In the **Clarizen Domain and URLs** section, perform the following steps:</span></span>

    ![Boxes for identifier and reply URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="3d656-153">a.</span><span class="sxs-lookup"><span data-stu-id="3d656-153">a.</span></span> <span data-ttu-id="3d656-154">In the **Identifier** box, type the value as: **Clarizen**</span><span class="sxs-lookup"><span data-stu-id="3d656-154">In the **Identifier** box, type the value as: **Clarizen**</span></span>

    <span data-ttu-id="3d656-155">b.</span><span class="sxs-lookup"><span data-stu-id="3d656-155">b.</span></span> <span data-ttu-id="3d656-156">In the **Reply URL** box, type a URL by using the following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="3d656-156">In the **Reply URL** box, type a URL by using the following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="3d656-157">These are not the real values.</span><span class="sxs-lookup"><span data-stu-id="3d656-157">These are not the real values.</span></span> <span data-ttu-id="3d656-158">You have to use the actual identifier and reply URL.</span><span class="sxs-lookup"><span data-stu-id="3d656-158">You have to use the actual identifier and reply URL.</span></span> <span data-ttu-id="3d656-159">Here we suggest that you use the unique value of a string as the identifier.</span><span class="sxs-lookup"><span data-stu-id="3d656-159">Here we suggest that you use the unique value of a string as the identifier.</span></span> <span data-ttu-id="3d656-160">To get the actual values, contact the [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span><span class="sxs-lookup"><span data-stu-id="3d656-160">To get the actual values, contact the [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="3d656-161">On the **SAML Signing Certificate** section, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="3d656-161">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Clicking "Create new certificate"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)     

5. <span data-ttu-id="3d656-163">In the **Create New Certificate** dialog box, click the calendar icon and select an expiry date.</span><span class="sxs-lookup"><span data-stu-id="3d656-163">In the **Create New Certificate** dialog box, click the calendar icon and select an expiry date.</span></span> <span data-ttu-id="3d656-164">Then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="3d656-164">Then click **Save**.</span></span>

    ![Selecting and saving an expiry date](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="3d656-166">In the **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="3d656-166">In the **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![Selecting the check box for making the new certificate active](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="3d656-168">In the **Rollover certificate** dialog box, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3d656-168">In the **Rollover certificate** dialog box, click **OK**.</span></span>

    ![Clicking "OK" to confirm that you want to make the certificate active](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="3d656-170">In the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="3d656-170">In the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Clicking "Certificate (Base64)" to start the download](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="3d656-172">In the **Clarizen Configuration** section, click **Configure Clarizen** to open the **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="3d656-172">In the **Clarizen Configuration** section, click **Configure Clarizen** to open the **Configure sign-on** window.</span></span>

    ![Clicking "Configure Clarizen"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    !["Configure sign-on" window, including files and URLs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="3d656-175">In a different web browser window, sign in to your Clarizen company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="3d656-175">In a different web browser window, sign in to your Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="3d656-176">Click your username, and then click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="3d656-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="3d656-177">![Clicking "Settings" under your username](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="3d656-177">![Clicking "Settings" under your username](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="3d656-178">Click the **Global Settings** tab. Then, next to **Federated Authentication**, click **edit**.</span><span class="sxs-lookup"><span data-stu-id="3d656-178">Click the **Global Settings** tab. Then, next to **Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="3d656-179">!["Global Settings" tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span><span class="sxs-lookup"><span data-stu-id="3d656-179">!["Global Settings" tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="3d656-180">In the **Federated Authentication** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3d656-180">In the **Federated Authentication** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="3d656-181">!["Federated Authentication" dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span><span class="sxs-lookup"><span data-stu-id="3d656-181">!["Federated Authentication" dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="3d656-182">a.</span><span class="sxs-lookup"><span data-stu-id="3d656-182">a.</span></span> <span data-ttu-id="3d656-183">Select **Enable Federated Authentication**.</span><span class="sxs-lookup"><span data-stu-id="3d656-183">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="3d656-184">b.</span><span class="sxs-lookup"><span data-stu-id="3d656-184">b.</span></span> <span data-ttu-id="3d656-185">Click **Upload** to upload your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="3d656-185">Click **Upload** to upload your downloaded certificate.</span></span>

    <span data-ttu-id="3d656-186">c.</span><span class="sxs-lookup"><span data-stu-id="3d656-186">c.</span></span> <span data-ttu-id="3d656-187">In the **Sign-in URL** box, enter the value of **SAML Single Sign-On Service URL** from the Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="3d656-187">In the **Sign-in URL** box, enter the value of **SAML Single Sign-On Service URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="3d656-188">d.</span><span class="sxs-lookup"><span data-stu-id="3d656-188">d.</span></span> <span data-ttu-id="3d656-189">In the **Sign-out URL** box, enter the value of **Sign-Out URL** from the Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="3d656-189">In the **Sign-out URL** box, enter the value of **Sign-Out URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="3d656-190">e.</span><span class="sxs-lookup"><span data-stu-id="3d656-190">e.</span></span> <span data-ttu-id="3d656-191">Select **Use POST**.</span><span class="sxs-lookup"><span data-stu-id="3d656-191">Select **Use POST**.</span></span>

    <span data-ttu-id="3d656-192">f.</span><span class="sxs-lookup"><span data-stu-id="3d656-192">f.</span></span> <span data-ttu-id="3d656-193">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="3d656-193">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3d656-194">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3d656-194">Create an Azure AD test user</span></span>
<span data-ttu-id="3d656-195">In the Azure portal, create a test user called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d656-195">In the Azure portal, create a test user called Britta Simon.</span></span>

![Name and email address of the Azure AD test user][100]

1. <span data-ttu-id="3d656-197">In the Azure portal, in the left pane, click the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="3d656-197">In the Azure portal, in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3d656-199">Click **Users and groups**, and then click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="3d656-199">Click **Users and groups**, and then click **All users** to display the list of users.</span></span>

    ![Clicking "Users and groups" and "All users"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3d656-201">At the top of the dialog box, click **Add** to open the **User** dialog box.</span><span class="sxs-lookup"><span data-stu-id="3d656-201">At the top of the dialog box, click **Add** to open the **User** dialog box.</span></span>

    ![The "Add" button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3d656-203">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3d656-203">In the **User** dialog box, perform the following steps:</span></span>

    !["User" dialog box with name, email address, and password filled in](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3d656-205">a.</span><span class="sxs-lookup"><span data-stu-id="3d656-205">a.</span></span> <span data-ttu-id="3d656-206">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3d656-206">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3d656-207">b.</span><span class="sxs-lookup"><span data-stu-id="3d656-207">b.</span></span> <span data-ttu-id="3d656-208">In the **User name** box, type the email address of the Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="3d656-208">In the **User name** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="3d656-209">c.</span><span class="sxs-lookup"><span data-stu-id="3d656-209">c.</span></span> <span data-ttu-id="3d656-210">Select **Show Password** and write down the value of **Password**.</span><span class="sxs-lookup"><span data-stu-id="3d656-210">Select **Show Password** and write down the value of **Password**.</span></span>

    <span data-ttu-id="3d656-211">d.</span><span class="sxs-lookup"><span data-stu-id="3d656-211">d.</span></span> <span data-ttu-id="3d656-212">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3d656-212">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="3d656-213">Create a Clarizen test user</span><span class="sxs-lookup"><span data-stu-id="3d656-213">Create a Clarizen test user</span></span>
<span data-ttu-id="3d656-214">To enable Azure AD users to sign in to Clarizen, you must provision user accounts.</span><span class="sxs-lookup"><span data-stu-id="3d656-214">To enable Azure AD users to sign in to Clarizen, you must provision user accounts.</span></span> <span data-ttu-id="3d656-215">In the case of Clarizen, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="3d656-215">In the case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="3d656-216">Sign in to your Clarizen company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="3d656-216">Sign in to your Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="3d656-217">Click **People**.</span><span class="sxs-lookup"><span data-stu-id="3d656-217">Click **People**.</span></span>

    <span data-ttu-id="3d656-218">![Clicking "People"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span><span class="sxs-lookup"><span data-stu-id="3d656-218">![Clicking "People"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="3d656-219">Click **Invite User**.</span><span class="sxs-lookup"><span data-stu-id="3d656-219">Click **Invite User**.</span></span>

    <span data-ttu-id="3d656-220">!["Invite User" button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span><span class="sxs-lookup"><span data-stu-id="3d656-220">!["Invite User" button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="3d656-221">In the **Invite People** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3d656-221">In the **Invite People** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="3d656-222">!["Invite People" dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span><span class="sxs-lookup"><span data-stu-id="3d656-222">!["Invite People" dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="3d656-223">a.</span><span class="sxs-lookup"><span data-stu-id="3d656-223">a.</span></span> <span data-ttu-id="3d656-224">In the **Email** box, type the email address of the Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="3d656-224">In the **Email** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="3d656-225">b.</span><span class="sxs-lookup"><span data-stu-id="3d656-225">b.</span></span> <span data-ttu-id="3d656-226">Click **Invite**.</span><span class="sxs-lookup"><span data-stu-id="3d656-226">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3d656-227">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="3d656-227">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3d656-228">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3d656-228">Assign the Azure AD test user</span></span>
<span data-ttu-id="3d656-229">Enable Britta Simon to use Azure single sign-on by granting her access to Clarizen.</span><span class="sxs-lookup"><span data-stu-id="3d656-229">Enable Britta Simon to use Azure single sign-on by granting her access to Clarizen.</span></span>

![Assigned test user][200]

1. <span data-ttu-id="3d656-231">In the Azure portal, open the applications view, browse to the directory view, click **Enterprise applications**, and then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3d656-231">In the Azure portal, open the applications view, browse to the directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![Clicking "Enterprise applications" and "All applications"][201]

2. <span data-ttu-id="3d656-233">In the applications list, select **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="3d656-233">In the applications list, select **Clarizen**.</span></span>

    ![Selecting Clarizen in the list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="3d656-235">In the left pane, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="3d656-235">In the left pane, click **Users and groups**.</span></span>

    ![Clicking "Users and groups"][202]

4. <span data-ttu-id="3d656-237">Click the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="3d656-237">Click the **Add** button.</span></span> <span data-ttu-id="3d656-238">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="3d656-238">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![The "Add" button and the "Add Assignment" dialog box][203]

5. <span data-ttu-id="3d656-240">In the **Users and groups** dialog box, select **Britta Simon** in the list of users.</span><span class="sxs-lookup"><span data-stu-id="3d656-240">In the **Users and groups** dialog box, select **Britta Simon** in the list of users.</span></span>

6. <span data-ttu-id="3d656-241">In the **Users and groups** dialog box, click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="3d656-241">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="3d656-242">In the **Add Assignment** dialog box, click the **Assign** button.</span><span class="sxs-lookup"><span data-stu-id="3d656-242">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="3d656-243">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="3d656-243">Test single sign-on</span></span>
<span data-ttu-id="3d656-244">Test your Azure AD single sign-on configuration by using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3d656-244">Test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="3d656-245">When you click the Clarizen tile in the Access Panel, you should be automatically signed in to your Clarizen application.</span><span class="sxs-lookup"><span data-stu-id="3d656-245">When you click the Clarizen tile in the Access Panel, you should be automatically signed in to your Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3d656-246">Additional resources</span><span class="sxs-lookup"><span data-stu-id="3d656-246">Additional resources</span></span>

* [<span data-ttu-id="3d656-247">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3d656-247">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3d656-248">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3d656-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png































