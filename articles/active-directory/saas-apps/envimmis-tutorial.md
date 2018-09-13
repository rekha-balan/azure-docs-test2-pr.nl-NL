---
title: 'Tutorial: Azure Active Directory integration with Envi MMIS | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Envi MMIS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab89f8ee-2507-4625-94bc-b24ef3d5e006
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2018
ms.author: jeedes
ms.openlocfilehash: 96168dcb8400d2580d0b64257ceb861c1da3ff65
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864363"
---
# <a name="tutorial-azure-active-directory-integration-with-envi-mmis"></a><span data-ttu-id="e579a-103">Tutorial: Azure Active Directory integration with Envi MMIS</span><span class="sxs-lookup"><span data-stu-id="e579a-103">Tutorial: Azure Active Directory integration with Envi MMIS</span></span>

<span data-ttu-id="e579a-104">In this tutorial, you learn how to integrate Envi MMIS with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e579a-104">In this tutorial, you learn how to integrate Envi MMIS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e579a-105">Integrating Envi MMIS with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e579a-105">Integrating Envi MMIS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e579a-106">You can control in Azure AD who has access to Envi MMIS.</span><span class="sxs-lookup"><span data-stu-id="e579a-106">You can control in Azure AD who has access to Envi MMIS.</span></span>
- <span data-ttu-id="e579a-107">You can enable your users to automatically get signed-on to Envi MMIS (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="e579a-107">You can enable your users to automatically get signed-on to Envi MMIS (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e579a-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e579a-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="e579a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="e579a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e579a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e579a-110">Prerequisites</span></span>

<span data-ttu-id="e579a-111">To configure Azure AD integration with Envi MMIS, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e579a-111">To configure Azure AD integration with Envi MMIS, you need the following items:</span></span>

- <span data-ttu-id="e579a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="e579a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e579a-113">An Envi MMIS single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e579a-113">An Envi MMIS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e579a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e579a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e579a-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="e579a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e579a-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="e579a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e579a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e579a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e579a-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="e579a-118">Scenario description</span></span>
<span data-ttu-id="e579a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e579a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e579a-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e579a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e579a-121">Adding Envi MMIS from the gallery</span><span class="sxs-lookup"><span data-stu-id="e579a-121">Adding Envi MMIS from the gallery</span></span>
1. <span data-ttu-id="e579a-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e579a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envi-mmis-from-the-gallery"></a><span data-ttu-id="e579a-123">Adding Envi MMIS from the gallery</span><span class="sxs-lookup"><span data-stu-id="e579a-123">Adding Envi MMIS from the gallery</span></span>
<span data-ttu-id="e579a-124">To configure the integration of Envi MMIS into Azure AD, you need to add Envi MMIS from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e579a-124">To configure the integration of Envi MMIS into Azure AD, you need to add Envi MMIS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e579a-125">**To add Envi MMIS from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e579a-125">**To add Envi MMIS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e579a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="e579a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="e579a-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="e579a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e579a-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e579a-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="e579a-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="e579a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="e579a-133">In the search box, type **Envi MMIS**, select **Envi MMIS** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="e579a-133">In the search box, type **Envi MMIS**, select **Envi MMIS** from result panel then click **Add** button to add the application.</span></span>

    ![Envi MMIS in the results list](./media/envimmis-tutorial/tutorial_envimmis_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e579a-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e579a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e579a-136">In this section, you configure and test Azure AD single sign-on with Envi MMIS based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e579a-136">In this section, you configure and test Azure AD single sign-on with Envi MMIS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e579a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Envi MMIS is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e579a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Envi MMIS is to a user in Azure AD.</span></span> <span data-ttu-id="e579a-138">In other words, a link relationship between an Azure AD user and the related user in Envi MMIS needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e579a-138">In other words, a link relationship between an Azure AD user and the related user in Envi MMIS needs to be established.</span></span>

<span data-ttu-id="e579a-139">To configure and test Azure AD single sign-on with Envi MMIS, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e579a-139">To configure and test Azure AD single sign-on with Envi MMIS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e579a-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e579a-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="e579a-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e579a-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="e579a-142">**[Create an Envi MMIS test user](#create-an-envi-mmis-test-user)** - to have a counterpart of Britta Simon in Envi MMIS that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="e579a-142">**[Create an Envi MMIS test user](#create-an-envi-mmis-test-user)** - to have a counterpart of Britta Simon in Envi MMIS that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="e579a-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e579a-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="e579a-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e579a-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e579a-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e579a-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e579a-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Envi MMIS application.</span><span class="sxs-lookup"><span data-stu-id="e579a-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Envi MMIS application.</span></span>

<span data-ttu-id="e579a-147">**To configure Azure AD single sign-on with Envi MMIS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e579a-147">**To configure Azure AD single sign-on with Envi MMIS, perform the following steps:**</span></span>

1. <span data-ttu-id="e579a-148">In the Azure portal, on the **Envi MMIS** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e579a-148">In the Azure portal, on the **Envi MMIS** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="e579a-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e579a-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/envimmis-tutorial/tutorial_envimmis_samlbase.png)

1. <span data-ttu-id="e579a-152">On the **Envi MMIS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="e579a-152">On the **Envi MMIS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Envi MMIS Domain and URLs single sign-on information](./media/envimmis-tutorial/tutorial_envimmis_url.png)

    <span data-ttu-id="e579a-154">a.</span><span class="sxs-lookup"><span data-stu-id="e579a-154">a.</span></span> <span data-ttu-id="e579a-155">In the **Identifier** textbox, type a URL using the following pattern: `https://www.<CUSTOMER DOMAIN>.com/Account`</span><span class="sxs-lookup"><span data-stu-id="e579a-155">In the **Identifier** textbox, type a URL using the following pattern: `https://www.<CUSTOMER DOMAIN>.com/Account`</span></span>

    <span data-ttu-id="e579a-156">b.</span><span class="sxs-lookup"><span data-stu-id="e579a-156">b.</span></span> <span data-ttu-id="e579a-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.<CUSTOMER DOMAIN>.com/Account/Acs`</span><span class="sxs-lookup"><span data-stu-id="e579a-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.<CUSTOMER DOMAIN>.com/Account/Acs`</span></span>

1. <span data-ttu-id="e579a-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="e579a-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Envi MMIS Domain and URLs single sign-on information](./media/envimmis-tutorial/tutorial_envimmis_url1.png)

    <span data-ttu-id="e579a-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.<CUSTOMER DOMAIN>.com/Account`</span><span class="sxs-lookup"><span data-stu-id="e579a-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.<CUSTOMER DOMAIN>.com/Account`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="e579a-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="e579a-161">These values are not real.</span></span> <span data-ttu-id="e579a-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="e579a-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="e579a-163">Contact [Envi MMIS Client support team](mailto:support@ioscorp.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="e579a-163">Contact [Envi MMIS Client support team](mailto:support@ioscorp.com) to get these values.</span></span>

1. <span data-ttu-id="e579a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="e579a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/envimmis-tutorial/tutorial_envimmis_certificate.png) 

1. <span data-ttu-id="e579a-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="e579a-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/envimmis-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="e579a-168">In a different web browser window, log into your Envi MMIS site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="e579a-168">In a different web browser window, log into your Envi MMIS site as an administrator.</span></span>

1. <span data-ttu-id="e579a-169">Click on **My Domain** tab.</span><span class="sxs-lookup"><span data-stu-id="e579a-169">Click on **My Domain** tab.</span></span>

    ![Configure Single Sign-On Save button](./media/envimmis-tutorial/configure1.png)

1. <span data-ttu-id="e579a-171">Click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="e579a-171">Click **Edit**.</span></span>

    ![Configure Single Sign-On Save button](./media/envimmis-tutorial/configure2.png)

1. <span data-ttu-id="e579a-173">Select **Use remote authentication** checkbox and then select **HTTP Redirect** from the **Authentication Type** dropdown.</span><span class="sxs-lookup"><span data-stu-id="e579a-173">Select **Use remote authentication** checkbox and then select **HTTP Redirect** from the **Authentication Type** dropdown.</span></span>

    ![Configure Single Sign-On Save button](./media/envimmis-tutorial/configure3.png)

1. <span data-ttu-id="e579a-175">Select **Resources** tab and then click **Upload Metadata**.</span><span class="sxs-lookup"><span data-stu-id="e579a-175">Select **Resources** tab and then click **Upload Metadata**.</span></span>

    ![Configure Single Sign-On Save button](./media/envimmis-tutorial/configure4.png)

1. <span data-ttu-id="e579a-177">In the **Upload Metadata** popup, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e579a-177">In the **Upload Metadata** popup, perform the following steps:</span></span>

    ![Configure Single Sign-On Save button](./media/envimmis-tutorial/configure5.png)

    <span data-ttu-id="e579a-179">a.</span><span class="sxs-lookup"><span data-stu-id="e579a-179">a.</span></span> <span data-ttu-id="e579a-180">Select **File** option from the **Upload From** dropdown.</span><span class="sxs-lookup"><span data-stu-id="e579a-180">Select **File** option from the **Upload From** dropdown.</span></span>

    <span data-ttu-id="e579a-181">b.</span><span class="sxs-lookup"><span data-stu-id="e579a-181">b.</span></span> <span data-ttu-id="e579a-182">Upload the downloaded metadata file from Azure portal by selecting the **choose file icon**.</span><span class="sxs-lookup"><span data-stu-id="e579a-182">Upload the downloaded metadata file from Azure portal by selecting the **choose file icon**.</span></span>

    <span data-ttu-id="e579a-183">c.</span><span class="sxs-lookup"><span data-stu-id="e579a-183">c.</span></span> <span data-ttu-id="e579a-184">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="e579a-184">Click **Ok**.</span></span>

1. <span data-ttu-id="e579a-185">After uploading the downloaded metadata file the fields will get populated automatically.</span><span class="sxs-lookup"><span data-stu-id="e579a-185">After uploading the downloaded metadata file the fields will get populated automatically.</span></span> <span data-ttu-id="e579a-186">Click **Update**</span><span class="sxs-lookup"><span data-stu-id="e579a-186">Click **Update**</span></span>

    ![Configure Single Sign-On Save button](./media/envimmis-tutorial/configure6.png)

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e579a-188">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e579a-188">Create an Azure AD test user</span></span>

<span data-ttu-id="e579a-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e579a-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="e579a-191">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e579a-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e579a-192">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="e579a-192">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/envimmis-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="e579a-194">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="e579a-194">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/envimmis-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="e579a-196">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="e579a-196">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/envimmis-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="e579a-198">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e579a-198">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/envimmis-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e579a-200">a.</span><span class="sxs-lookup"><span data-stu-id="e579a-200">a.</span></span> <span data-ttu-id="e579a-201">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e579a-201">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e579a-202">b.</span><span class="sxs-lookup"><span data-stu-id="e579a-202">b.</span></span> <span data-ttu-id="e579a-203">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e579a-203">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="e579a-204">c.</span><span class="sxs-lookup"><span data-stu-id="e579a-204">c.</span></span> <span data-ttu-id="e579a-205">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="e579a-205">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="e579a-206">d.</span><span class="sxs-lookup"><span data-stu-id="e579a-206">d.</span></span> <span data-ttu-id="e579a-207">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e579a-207">Click **Create**.</span></span>
 
### <a name="create-an-envi-mmis-test-user"></a><span data-ttu-id="e579a-208">Create an Envi MMIS test user</span><span class="sxs-lookup"><span data-stu-id="e579a-208">Create an Envi MMIS test user</span></span>

<span data-ttu-id="e579a-209">To enable Azure AD users to log in to Envi MMIS, they must be provisioned into Envi MMIS.</span><span class="sxs-lookup"><span data-stu-id="e579a-209">To enable Azure AD users to log in to Envi MMIS, they must be provisioned into Envi MMIS.</span></span>  
<span data-ttu-id="e579a-210">In the case of Envi MMIS, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="e579a-210">In the case of Envi MMIS, provisioning is a manual task.</span></span>

<span data-ttu-id="e579a-211">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e579a-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="e579a-212">Log in to your Envi MMIS company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="e579a-212">Log in to your Envi MMIS company site as an administrator.</span></span>

1. <span data-ttu-id="e579a-213">Click on **User List** tab.</span><span class="sxs-lookup"><span data-stu-id="e579a-213">Click on **User List** tab.</span></span>

    ![Add Employee](./media/envimmis-tutorial/user1.png)

1. <span data-ttu-id="e579a-215">Click **Add User** button.</span><span class="sxs-lookup"><span data-stu-id="e579a-215">Click **Add User** button.</span></span>

    ![Add Employee](./media/envimmis-tutorial/user2.png)

1. <span data-ttu-id="e579a-217">In the **Add User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e579a-217">In the **Add User** section, perform the following steps:</span></span>

    ![Add Employee](./media/envimmis-tutorial/user3.png)

    <span data-ttu-id="e579a-219">a.</span><span class="sxs-lookup"><span data-stu-id="e579a-219">a.</span></span> <span data-ttu-id="e579a-220">In the **User Name** textbox, type the username of Britta Simon account like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="e579a-220">In the **User Name** textbox, type the username of Britta Simon account like **brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="e579a-221">b.</span><span class="sxs-lookup"><span data-stu-id="e579a-221">b.</span></span> <span data-ttu-id="e579a-222">In the **First Name** textbox, type the first name of BrittaSimon like **Britta**.</span><span class="sxs-lookup"><span data-stu-id="e579a-222">In the **First Name** textbox, type the first name of BrittaSimon like **Britta**.</span></span>

    <span data-ttu-id="e579a-223">c.</span><span class="sxs-lookup"><span data-stu-id="e579a-223">c.</span></span> <span data-ttu-id="e579a-224">In the **Last Name** textbox, type the last name of BrittaSimon like **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e579a-224">In the **Last Name** textbox, type the last name of BrittaSimon like **Simon**.</span></span>

    <span data-ttu-id="e579a-225">d.</span><span class="sxs-lookup"><span data-stu-id="e579a-225">d.</span></span> <span data-ttu-id="e579a-226">Enter the Title of the user in the **Title** of the textbox.</span><span class="sxs-lookup"><span data-stu-id="e579a-226">Enter the Title of the user in the **Title** of the textbox.</span></span>
    
    <span data-ttu-id="e579a-227">e.</span><span class="sxs-lookup"><span data-stu-id="e579a-227">e.</span></span> <span data-ttu-id="e579a-228">In the **Email Address** textbox, type the email address of Britta Simon account like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="e579a-228">In the **Email Address** textbox, type the email address of Britta Simon account like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="e579a-229">f.</span><span class="sxs-lookup"><span data-stu-id="e579a-229">f.</span></span> <span data-ttu-id="e579a-230">In the **SSO User Name** textbox, type the username of Britta Simon account like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="e579a-230">In the **SSO User Name** textbox, type the username of Britta Simon account like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="e579a-231">g.</span><span class="sxs-lookup"><span data-stu-id="e579a-231">g.</span></span> <span data-ttu-id="e579a-232">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e579a-232">Click **Save**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e579a-233">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e579a-233">Assign the Azure AD test user</span></span>

<span data-ttu-id="e579a-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Envi MMIS.</span><span class="sxs-lookup"><span data-stu-id="e579a-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Envi MMIS.</span></span>

![Assign the user role][200] 

<span data-ttu-id="e579a-236">**To assign Britta Simon to Envi MMIS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e579a-236">**To assign Britta Simon to Envi MMIS, perform the following steps:**</span></span>

1. <span data-ttu-id="e579a-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e579a-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="e579a-239">In the applications list, select **Envi MMIS**.</span><span class="sxs-lookup"><span data-stu-id="e579a-239">In the applications list, select **Envi MMIS**.</span></span>

    ![The Envi MMIS link in the Applications list](./media/envimmis-tutorial/tutorial_envimmis_app.png)  

1. <span data-ttu-id="e579a-241">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="e579a-241">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="e579a-243">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="e579a-243">Click **Add** button.</span></span> <span data-ttu-id="e579a-244">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e579a-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="e579a-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="e579a-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="e579a-247">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="e579a-247">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="e579a-248">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e579a-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e579a-249">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="e579a-249">Test single sign-on</span></span>

<span data-ttu-id="e579a-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e579a-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e579a-251">When you click the Envi MMIS tile in the Access Panel, you should get automatically signed-on to your Envi MMIS application.</span><span class="sxs-lookup"><span data-stu-id="e579a-251">When you click the Envi MMIS tile in the Access Panel, you should get automatically signed-on to your Envi MMIS application.</span></span>
<span data-ttu-id="e579a-252">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e579a-252">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e579a-253">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e579a-253">Additional resources</span></span>

* [<span data-ttu-id="e579a-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e579a-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="e579a-255">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e579a-255">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/envimmis-tutorial/tutorial_general_01.png
[2]: ./media/envimmis-tutorial/tutorial_general_02.png
[3]: ./media/envimmis-tutorial/tutorial_general_03.png
[4]: ./media/envimmis-tutorial/tutorial_general_04.png

[100]: ./media/envimmis-tutorial/tutorial_general_100.png

[200]: ./media/envimmis-tutorial/tutorial_general_200.png
[201]: ./media/envimmis-tutorial/tutorial_general_201.png
[202]: ./media/envimmis-tutorial/tutorial_general_202.png
[203]: ./media/envimmis-tutorial/tutorial_general_203.png

