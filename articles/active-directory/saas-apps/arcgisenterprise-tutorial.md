---
title: 'Tutorial: Azure Active Directory integration with ArcGIS Enterprise | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ArcGIS Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 24809e9d-a4aa-4504-95a9-e4fcf484f431
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2018
ms.author: jeedes
ms.openlocfilehash: ea2b32b43fedacba7b8a60db29762c32fda65aa5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968835"
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-enterprise"></a><span data-ttu-id="f19e1-103">Tutorial: Azure Active Directory integration with ArcGIS Enterprise</span><span class="sxs-lookup"><span data-stu-id="f19e1-103">Tutorial: Azure Active Directory integration with ArcGIS Enterprise</span></span>

<span data-ttu-id="f19e1-104">In this tutorial, you learn how to integrate ArcGIS Enterprise with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f19e1-104">In this tutorial, you learn how to integrate ArcGIS Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f19e1-105">Integrating ArcGIS Enterprise with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f19e1-105">Integrating ArcGIS Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f19e1-106">You can control in Azure AD who has access to ArcGIS Enterprise.</span><span class="sxs-lookup"><span data-stu-id="f19e1-106">You can control in Azure AD who has access to ArcGIS Enterprise.</span></span>
- <span data-ttu-id="f19e1-107">You can enable your users to automatically get signed-on to ArcGIS Enterprise (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="f19e1-107">You can enable your users to automatically get signed-on to ArcGIS Enterprise (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f19e1-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f19e1-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f19e1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span><span class="sxs-lookup"><span data-stu-id="f19e1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f19e1-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f19e1-110">Prerequisites</span></span>

<span data-ttu-id="f19e1-111">To configure Azure AD integration with ArcGIS Enterprise, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f19e1-111">To configure Azure AD integration with ArcGIS Enterprise, you need the following items:</span></span>

- <span data-ttu-id="f19e1-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f19e1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f19e1-113">An ArcGIS Enterprise single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f19e1-113">An ArcGIS Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f19e1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f19e1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f19e1-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f19e1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f19e1-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="f19e1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f19e1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f19e1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f19e1-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f19e1-118">Scenario description</span></span>

<span data-ttu-id="f19e1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f19e1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f19e1-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f19e1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f19e1-121">Adding ArcGIS Enterprise from the gallery</span><span class="sxs-lookup"><span data-stu-id="f19e1-121">Adding ArcGIS Enterprise from the gallery</span></span>
2. <span data-ttu-id="f19e1-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f19e1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-enterprise-from-the-gallery"></a><span data-ttu-id="f19e1-123">Adding ArcGIS Enterprise from the gallery</span><span class="sxs-lookup"><span data-stu-id="f19e1-123">Adding ArcGIS Enterprise from the gallery</span></span>

<span data-ttu-id="f19e1-124">To configure the integration of ArcGIS Enterprise into Azure AD, you need to add ArcGIS Enterprise from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f19e1-124">To configure the integration of ArcGIS Enterprise into Azure AD, you need to add ArcGIS Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f19e1-125">**To add ArcGIS Enterprise from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f19e1-125">**To add ArcGIS Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f19e1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f19e1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="f19e1-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="f19e1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f19e1-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f19e1-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="f19e1-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="f19e1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="f19e1-133">In the search box, type **ArcGIS Enterprise**, select **ArcGIS Enterprise** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="f19e1-133">In the search box, type **ArcGIS Enterprise**, select **ArcGIS Enterprise** from result panel then click **Add** button to add the application.</span></span>

    ![ArcGIS Enterprise in the results list](./media/arcgisenterprise-tutorial/tutorial_arcgisenterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f19e1-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f19e1-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f19e1-136">In this section, you configure and test Azure AD single sign-on with ArcGIS Enterprise based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f19e1-136">In this section, you configure and test Azure AD single sign-on with ArcGIS Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f19e1-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ArcGIS Enterprise is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f19e1-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ArcGIS Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="f19e1-138">In other words, a link relationship between an Azure AD user and the related user in ArcGIS Enterprise needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f19e1-138">In other words, a link relationship between an Azure AD user and the related user in ArcGIS Enterprise needs to be established.</span></span>

<span data-ttu-id="f19e1-139">To configure and test Azure AD single sign-on with ArcGIS Enterprise, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f19e1-139">To configure and test Azure AD single sign-on with ArcGIS Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f19e1-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f19e1-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f19e1-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f19e1-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f19e1-142">**[Create an ArcGIS Enterprise test user](#create-an-arcgis-enterprise-test-user)** - to have a counterpart of Britta Simon in ArcGIS Enterprise that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="f19e1-142">**[Create an ArcGIS Enterprise test user](#create-an-arcgis-enterprise-test-user)** - to have a counterpart of Britta Simon in ArcGIS Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f19e1-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f19e1-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f19e1-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f19e1-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f19e1-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f19e1-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f19e1-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ArcGIS Enterprise application.</span><span class="sxs-lookup"><span data-stu-id="f19e1-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ArcGIS Enterprise application.</span></span>

<span data-ttu-id="f19e1-147">**To configure Azure AD single sign-on with ArcGIS Enterprise, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f19e1-147">**To configure Azure AD single sign-on with ArcGIS Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="f19e1-148">In the Azure portal, on the **ArcGIS Enterprise** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f19e1-148">In the Azure portal, on the **ArcGIS Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="f19e1-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f19e1-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/arcgisenterprise-tutorial/tutorial_arcgisenterprise_samlbase.png)

3. <span data-ttu-id="f19e1-152">On the **ArcGIS Enterprise Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="f19e1-152">On the **ArcGIS Enterprise Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![ArcGIS Enterprise Domain and URLs single sign-on information](./media/arcgisenterprise-tutorial/tutorial_arcgisenterprise_url1.png)

    <span data-ttu-id="f19e1-154">a.</span><span class="sxs-lookup"><span data-stu-id="f19e1-154">a.</span></span> <span data-ttu-id="f19e1-155">In the **Identifier** textbox, type a URL using the following pattern: `<EXTERNAL_DNS_NAME>.portal`</span><span class="sxs-lookup"><span data-stu-id="f19e1-155">In the **Identifier** textbox, type a URL using the following pattern: `<EXTERNAL_DNS_NAME>.portal`</span></span>

    <span data-ttu-id="f19e1-156">b.</span><span class="sxs-lookup"><span data-stu-id="f19e1-156">b.</span></span> <span data-ttu-id="f19e1-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<EXTERNAL_DNS_NAME>/portal/sharing/rest/oauth2/saml/signin2`</span><span class="sxs-lookup"><span data-stu-id="f19e1-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<EXTERNAL_DNS_NAME>/portal/sharing/rest/oauth2/saml/signin2`</span></span>

4. <span data-ttu-id="f19e1-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="f19e1-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![ArcGIS Enterprise Domain and URLs single sign-on information](./media/arcgisenterprise-tutorial/tutorial_arcgisenterprise_url2.png)

    <span data-ttu-id="f19e1-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<EXTERNAL_DNS_NAME>/portal/sharing/rest/oauth2/saml/signin`</span><span class="sxs-lookup"><span data-stu-id="f19e1-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<EXTERNAL_DNS_NAME>/portal/sharing/rest/oauth2/saml/signin`</span></span>

    > [!NOTE]
    > <span data-ttu-id="f19e1-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="f19e1-161">These values are not real.</span></span> <span data-ttu-id="f19e1-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="f19e1-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="f19e1-163">Contact [ArcGIS Enterprise Client support team](mailto:support@esri.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="f19e1-163">Contact [ArcGIS Enterprise Client support team](mailto:support@esri.com) to get these values.</span></span> <span data-ttu-id="f19e1-164">You will get the Identifier value from **Set Identity Provider** section, which is explained later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="f19e1-164">You will get the Identifier value from **Set Identity Provider** section, which is explained later in this tutorial.</span></span>

5. <span data-ttu-id="f19e1-165">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="f19e1-165">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

    ![The Certificate download link](./media/arcgisenterprise-tutorial/tutorial_arcgisenterprise_certificate.png)

6. <span data-ttu-id="f19e1-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="f19e1-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/arcgisenterprise-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f19e1-169">In a different web browser window, log in to your ArcGIS Enterprise company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f19e1-169">In a different web browser window, log in to your ArcGIS Enterprise company site as an administrator.</span></span>

8. <span data-ttu-id="f19e1-170">Select **Organization >EDIT SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="f19e1-170">Select **Organization >EDIT SETTINGS**.</span></span>

    ![ArcGIS Enterprise Configuration](./media/arcgisenterprise-tutorial/configure1.png)

9. <span data-ttu-id="f19e1-172">Select **Security** tab.</span><span class="sxs-lookup"><span data-stu-id="f19e1-172">Select **Security** tab.</span></span>

    ![ArcGIS Enterprise Configuration](./media/arcgisenterprise-tutorial/configure2.png)

10. <span data-ttu-id="f19e1-174">Scroll down to the **Enterprise Logins via SAML** section and select **SET ENTERPRISE LOGIN**.</span><span class="sxs-lookup"><span data-stu-id="f19e1-174">Scroll down to the **Enterprise Logins via SAML** section and select **SET ENTERPRISE LOGIN**.</span></span>

    ![ArcGIS Enterprise Configuration](./media/arcgisenterprise-tutorial/configure3.png)

11. <span data-ttu-id="f19e1-176">On the **Set Identity Provider** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f19e1-176">On the **Set Identity Provider** section, perform the following steps:</span></span>

    ![ArcGIS Enterprise Configuration](./media/arcgisenterprise-tutorial/configure4.png)

    <span data-ttu-id="f19e1-178">a.</span><span class="sxs-lookup"><span data-stu-id="f19e1-178">a.</span></span> <span data-ttu-id="f19e1-179">Please provide a name like **Azure Active Directory Test** in the **Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="f19e1-179">Please provide a name like **Azure Active Directory Test** in the **Name** textbox.</span></span>

    <span data-ttu-id="f19e1-180">b.</span><span class="sxs-lookup"><span data-stu-id="f19e1-180">b.</span></span> <span data-ttu-id="f19e1-181">In the **URL** textbox, paste the **App Federation Metadata Url** value which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f19e1-181">In the **URL** textbox, paste the **App Federation Metadata Url** value which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="f19e1-182">c.</span><span class="sxs-lookup"><span data-stu-id="f19e1-182">c.</span></span> <span data-ttu-id="f19e1-183">Click **Show advanced settings** and copy the **Entity ID** value and paste it into the **Identifier** textbox in the **ArcGIS Enterprise Domain and URLs** section in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f19e1-183">Click **Show advanced settings** and copy the **Entity ID** value and paste it into the **Identifier** textbox in the **ArcGIS Enterprise Domain and URLs** section in Azure portal.</span></span>
    
    ![ArcGIS Enterprise Configuration](./media/arcgisenterprise-tutorial/configure5.png)

    <span data-ttu-id="f19e1-185">d.</span><span class="sxs-lookup"><span data-stu-id="f19e1-185">d.</span></span> <span data-ttu-id="f19e1-186">Click **UPDATE IDENTITY PROVIDER**.</span><span class="sxs-lookup"><span data-stu-id="f19e1-186">Click **UPDATE IDENTITY PROVIDER**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f19e1-187">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f19e1-187">Create an Azure AD test user</span></span>

<span data-ttu-id="f19e1-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f19e1-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="f19e1-190">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f19e1-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f19e1-191">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="f19e1-191">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/arcgisenterprise-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f19e1-193">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="f19e1-193">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/arcgisenterprise-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f19e1-195">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="f19e1-195">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/arcgisenterprise-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f19e1-197">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f19e1-197">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/arcgisenterprise-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f19e1-199">a.</span><span class="sxs-lookup"><span data-stu-id="f19e1-199">a.</span></span> <span data-ttu-id="f19e1-200">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f19e1-200">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f19e1-201">b.</span><span class="sxs-lookup"><span data-stu-id="f19e1-201">b.</span></span> <span data-ttu-id="f19e1-202">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f19e1-202">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f19e1-203">c.</span><span class="sxs-lookup"><span data-stu-id="f19e1-203">c.</span></span> <span data-ttu-id="f19e1-204">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="f19e1-204">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f19e1-205">d.</span><span class="sxs-lookup"><span data-stu-id="f19e1-205">d.</span></span> <span data-ttu-id="f19e1-206">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f19e1-206">Click **Create**.</span></span>

### <a name="create-an-arcgis-enterprise-test-user"></a><span data-ttu-id="f19e1-207">Create an ArcGIS Enterprise test user</span><span class="sxs-lookup"><span data-stu-id="f19e1-207">Create an ArcGIS Enterprise test user</span></span>

<span data-ttu-id="f19e1-208">The objective of this section is to create a user called Britta Simon in ArcGIS Enterprise.</span><span class="sxs-lookup"><span data-stu-id="f19e1-208">The objective of this section is to create a user called Britta Simon in ArcGIS Enterprise.</span></span> <span data-ttu-id="f19e1-209">ArcGIS Enterprise supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="f19e1-209">ArcGIS Enterprise supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="f19e1-210">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="f19e1-210">There is no action item for you in this section.</span></span> <span data-ttu-id="f19e1-211">A new user is created during an attempt to access ArcGIS Enterprise if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="f19e1-211">A new user is created during an attempt to access ArcGIS Enterprise if it doesn't exist yet.</span></span>

> [!Note]
> <span data-ttu-id="f19e1-212">If you need to create a user manually, contact [ArcGIS Enterprise support team](mailto:support@esri.com).</span><span class="sxs-lookup"><span data-stu-id="f19e1-212">If you need to create a user manually, contact [ArcGIS Enterprise support team](mailto:support@esri.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f19e1-213">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f19e1-213">Assign the Azure AD test user</span></span>

<span data-ttu-id="f19e1-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ArcGIS Enterprise.</span><span class="sxs-lookup"><span data-stu-id="f19e1-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ArcGIS Enterprise.</span></span>

![Assign the user role][200]

<span data-ttu-id="f19e1-216">**To assign Britta Simon to ArcGIS Enterprise, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f19e1-216">**To assign Britta Simon to ArcGIS Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="f19e1-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f19e1-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="f19e1-219">In the applications list, select **ArcGIS Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="f19e1-219">In the applications list, select **ArcGIS Enterprise**.</span></span>

    ![The ArcGIS Enterprise link in the Applications list](./media/arcgisenterprise-tutorial/tutorial_arcgisenterprise_app.png)  

3. <span data-ttu-id="f19e1-221">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f19e1-221">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="f19e1-223">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="f19e1-223">Click **Add** button.</span></span> <span data-ttu-id="f19e1-224">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f19e1-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="f19e1-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="f19e1-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f19e1-227">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="f19e1-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f19e1-228">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f19e1-228">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="f19e1-229">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="f19e1-229">Test single sign-on</span></span>

<span data-ttu-id="f19e1-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f19e1-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f19e1-231">When you click the ArcGIS Enterprise tile in the Access Panel, you should get automatically signed-on to your ArcGIS Enterprise application.</span><span class="sxs-lookup"><span data-stu-id="f19e1-231">When you click the ArcGIS Enterprise tile in the Access Panel, you should get automatically signed-on to your ArcGIS Enterprise application.</span></span>
<span data-ttu-id="f19e1-232">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f19e1-232">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f19e1-233">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f19e1-233">Additional resources</span></span>

* [<span data-ttu-id="f19e1-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f19e1-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="f19e1-235">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f19e1-235">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/arcgisenterprise-tutorial/tutorial_general_01.png
[2]: ./media/arcgisenterprise-tutorial/tutorial_general_02.png
[3]: ./media/arcgisenterprise-tutorial/tutorial_general_03.png
[4]: ./media/arcgisenterprise-tutorial/tutorial_general_04.png

[100]: ./media/arcgisenterprise-tutorial/tutorial_general_100.png

[200]: ./media/arcgisenterprise-tutorial/tutorial_general_200.png
[201]: ./media/arcgisenterprise-tutorial/tutorial_general_201.png
[202]: ./media/arcgisenterprise-tutorial/tutorial_general_202.png
[203]: ./media/arcgisenterprise-tutorial/tutorial_general_203.png