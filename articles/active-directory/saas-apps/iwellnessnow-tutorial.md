---
title: 'Tutorial: Azure Active Directory integration with iWellnessNow | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and iWellnessNow.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 24ffc841-7a77-481c-9cc4-6f8bda58fe66
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2018
ms.author: jeedes
ms.openlocfilehash: c260b32dc6f659ca4cc1b4c3f59859f75ba999d0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866268"
---
# <a name="tutorial-azure-active-directory-integration-with-iwellnessnow"></a><span data-ttu-id="48be2-103">Tutorial: Azure Active Directory integration with iWellnessNow</span><span class="sxs-lookup"><span data-stu-id="48be2-103">Tutorial: Azure Active Directory integration with iWellnessNow</span></span>

<span data-ttu-id="48be2-104">In this tutorial, you learn how to integrate iWellnessNow with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="48be2-104">In this tutorial, you learn how to integrate iWellnessNow with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="48be2-105">Integrating iWellnessNow with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="48be2-105">Integrating iWellnessNow with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="48be2-106">You can control in Azure AD who has access to iWellnessNow.</span><span class="sxs-lookup"><span data-stu-id="48be2-106">You can control in Azure AD who has access to iWellnessNow.</span></span>
- <span data-ttu-id="48be2-107">You can enable your users to automatically get signed-on to iWellnessNow (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="48be2-107">You can enable your users to automatically get signed-on to iWellnessNow (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="48be2-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="48be2-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="48be2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="48be2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48be2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="48be2-110">Prerequisites</span></span>

<span data-ttu-id="48be2-111">To configure Azure AD integration with iWellnessNow, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="48be2-111">To configure Azure AD integration with iWellnessNow, you need the following items:</span></span>

- <span data-ttu-id="48be2-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="48be2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="48be2-113">An iWellnessNow single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="48be2-113">An iWellnessNow single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="48be2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="48be2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="48be2-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="48be2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="48be2-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="48be2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="48be2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48be2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="48be2-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="48be2-118">Scenario description</span></span>
<span data-ttu-id="48be2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="48be2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="48be2-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="48be2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="48be2-121">Adding iWellnessNow from the gallery</span><span class="sxs-lookup"><span data-stu-id="48be2-121">Adding iWellnessNow from the gallery</span></span>
1. <span data-ttu-id="48be2-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="48be2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-iwellnessnow-from-the-gallery"></a><span data-ttu-id="48be2-123">Adding iWellnessNow from the gallery</span><span class="sxs-lookup"><span data-stu-id="48be2-123">Adding iWellnessNow from the gallery</span></span>
<span data-ttu-id="48be2-124">To configure the integration of iWellnessNow into Azure AD, you need to add iWellnessNow from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="48be2-124">To configure the integration of iWellnessNow into Azure AD, you need to add iWellnessNow from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="48be2-125">**To add iWellnessNow from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="48be2-125">**To add iWellnessNow from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="48be2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="48be2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="48be2-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="48be2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="48be2-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="48be2-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="48be2-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="48be2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="48be2-133">In the search box, type **iWellnessNow**, select **iWellnessNow** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="48be2-133">In the search box, type **iWellnessNow**, select **iWellnessNow** from result panel then click **Add** button to add the application.</span></span>

    ![iWellnessNow in the results list](./media/iwellnessnow-tutorial/tutorial_iwellnessnow_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="48be2-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="48be2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="48be2-136">In this section, you configure and test Azure AD single sign-on with iWellnessNow based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="48be2-136">In this section, you configure and test Azure AD single sign-on with iWellnessNow based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="48be2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in iWellnessNow is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48be2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in iWellnessNow is to a user in Azure AD.</span></span> <span data-ttu-id="48be2-138">In other words, a link relationship between an Azure AD user and the related user in iWellnessNow needs to be established.</span><span class="sxs-lookup"><span data-stu-id="48be2-138">In other words, a link relationship between an Azure AD user and the related user in iWellnessNow needs to be established.</span></span>

<span data-ttu-id="48be2-139">To configure and test Azure AD single sign-on with iWellnessNow, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="48be2-139">To configure and test Azure AD single sign-on with iWellnessNow, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="48be2-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="48be2-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="48be2-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48be2-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="48be2-142">**[Create an iWellnessNow test user](#create-an-iwellnessnow-test-user)** - to have a counterpart of Britta Simon in iWellnessNow that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="48be2-142">**[Create an iWellnessNow test user](#create-an-iwellnessnow-test-user)** - to have a counterpart of Britta Simon in iWellnessNow that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="48be2-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="48be2-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="48be2-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="48be2-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="48be2-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="48be2-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="48be2-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your iWellnessNow application.</span><span class="sxs-lookup"><span data-stu-id="48be2-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your iWellnessNow application.</span></span>

<span data-ttu-id="48be2-147">**To configure Azure AD single sign-on with iWellnessNow, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="48be2-147">**To configure Azure AD single sign-on with iWellnessNow, perform the following steps:**</span></span>

1. <span data-ttu-id="48be2-148">In the Azure portal, on the **iWellnessNow** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="48be2-148">In the Azure portal, on the **iWellnessNow** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="48be2-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="48be2-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/iwellnessnow-tutorial/tutorial_iwellnessnow_samlbase.png)

1. <span data-ttu-id="48be2-152">On the **iWellnessNow Domain and URLs** section, if you have **Service Provider metadata file** and wish to configure the application in **IDP** initiated mode, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="48be2-152">On the **iWellnessNow Domain and URLs** section, if you have **Service Provider metadata file** and wish to configure the application in **IDP** initiated mode, perform the following steps:</span></span>

    ![iWellnessNow Domain and URLs single sign-on upload](./media/iwellnessnow-tutorial/tutorial_iwellnessnow_upload.png)

    <span data-ttu-id="48be2-154">a.</span><span class="sxs-lookup"><span data-stu-id="48be2-154">a.</span></span> <span data-ttu-id="48be2-155">Click **Upload metadata file**.</span><span class="sxs-lookup"><span data-stu-id="48be2-155">Click **Upload metadata file**.</span></span>

    ![iWellnessNow Domain and URLs single sign-on uploadconfig](./media/iwellnessnow-tutorial/tutorial_iwellnessnow_uploadconfig.png)

    <span data-ttu-id="48be2-157">b.</span><span class="sxs-lookup"><span data-stu-id="48be2-157">b.</span></span> <span data-ttu-id="48be2-158">Click on **folder logo** to select the metadata file and click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="48be2-158">Click on **folder logo** to select the metadata file and click **Upload**.</span></span>
    
    <span data-ttu-id="48be2-159">c.</span><span class="sxs-lookup"><span data-stu-id="48be2-159">c.</span></span> <span data-ttu-id="48be2-160">After successfull completion of uploading **Service Provider metadata file** the **Identifier** and **Reply URL** values get auto populated in **iWellnessNow Domain and URLs** section textbox as shown below:</span><span class="sxs-lookup"><span data-stu-id="48be2-160">After successfull completion of uploading **Service Provider metadata file** the **Identifier** and **Reply URL** values get auto populated in **iWellnessNow Domain and URLs** section textbox as shown below:</span></span>

    ![iWellnessNow Domain and URLs single sign-on information](./media/iwellnessnow-tutorial/tutorial_iwellnessnow_url3.png)

1. <span data-ttu-id="48be2-162">If you dont have **Service Provider metadata file** and wish to configure the application in **IDP** initiated mode, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="48be2-162">If you dont have **Service Provider metadata file** and wish to configure the application in **IDP** initiated mode, perform the following steps:</span></span>

    ![iWellnessNow Domain and URLs single sign-on information](./media/iwellnessnow-tutorial/tutorial_iwellnessnow_url.png)

    <span data-ttu-id="48be2-164">a.</span><span class="sxs-lookup"><span data-stu-id="48be2-164">a.</span></span> <span data-ttu-id="48be2-165">In the **Identifier** textbox, type a URL using the following pattern: `http://<CustomerName>.iwellnessnow.com`</span><span class="sxs-lookup"><span data-stu-id="48be2-165">In the **Identifier** textbox, type a URL using the following pattern: `http://<CustomerName>.iwellnessnow.com`</span></span>

    <span data-ttu-id="48be2-166">b.</span><span class="sxs-lookup"><span data-stu-id="48be2-166">b.</span></span> <span data-ttu-id="48be2-167">In the **Reply URL** textbox, type a URL using the following pattern: `https://<CustomerName>.iwellnessnow.com/ssologin`</span><span class="sxs-lookup"><span data-stu-id="48be2-167">In the **Reply URL** textbox, type a URL using the following pattern: `https://<CustomerName>.iwellnessnow.com/ssologin`</span></span>

1. <span data-ttu-id="48be2-168">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="48be2-168">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![iWellnessNow Domain and URLs single sign-on information](./media/iwellnessnow-tutorial/tutorial_iwellnessnow_url1.png)

    <span data-ttu-id="48be2-170">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<CustomerName>.iwellnessnow.com/`</span><span class="sxs-lookup"><span data-stu-id="48be2-170">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<CustomerName>.iwellnessnow.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="48be2-171">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="48be2-171">These values are not real.</span></span> <span data-ttu-id="48be2-172">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="48be2-172">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="48be2-173">Contact [iWellnessNow Client support team](mailto:info@iwellnessnow.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="48be2-173">Contact [iWellnessNow Client support team](mailto:info@iwellnessnow.com) to get these values.</span></span>

1. <span data-ttu-id="48be2-174">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="48be2-174">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/iwellnessnow-tutorial/tutorial_iwellnessnow_certificate.png) 

1. <span data-ttu-id="48be2-176">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="48be2-176">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/iwellnessnow-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="48be2-178">To configure single sign-on on **iWellnessNow** side, you need to send the downloaded **Metadata XML** to [iWellnessNow support team](mailto:info@iwellnessnow.com).</span><span class="sxs-lookup"><span data-stu-id="48be2-178">To configure single sign-on on **iWellnessNow** side, you need to send the downloaded **Metadata XML** to [iWellnessNow support team](mailto:info@iwellnessnow.com).</span></span> <span data-ttu-id="48be2-179">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="48be2-179">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="48be2-180">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="48be2-180">Create an Azure AD test user</span></span>

<span data-ttu-id="48be2-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48be2-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="48be2-183">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="48be2-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="48be2-184">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="48be2-184">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/iwellnessnow-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="48be2-186">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="48be2-186">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/iwellnessnow-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="48be2-188">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="48be2-188">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/iwellnessnow-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="48be2-190">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="48be2-190">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/iwellnessnow-tutorial/create_aaduser_04.png)

    <span data-ttu-id="48be2-192">a.</span><span class="sxs-lookup"><span data-stu-id="48be2-192">a.</span></span> <span data-ttu-id="48be2-193">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="48be2-193">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="48be2-194">b.</span><span class="sxs-lookup"><span data-stu-id="48be2-194">b.</span></span> <span data-ttu-id="48be2-195">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48be2-195">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="48be2-196">c.</span><span class="sxs-lookup"><span data-stu-id="48be2-196">c.</span></span> <span data-ttu-id="48be2-197">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="48be2-197">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="48be2-198">d.</span><span class="sxs-lookup"><span data-stu-id="48be2-198">d.</span></span> <span data-ttu-id="48be2-199">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="48be2-199">Click **Create**.</span></span>
 
### <a name="create-an-iwellnessnow-test-user"></a><span data-ttu-id="48be2-200">Create an iWellnessNow test user</span><span class="sxs-lookup"><span data-stu-id="48be2-200">Create an iWellnessNow test user</span></span>

<span data-ttu-id="48be2-201">In this section, you create a user called Britta Simon in iWellnessNow.</span><span class="sxs-lookup"><span data-stu-id="48be2-201">In this section, you create a user called Britta Simon in iWellnessNow.</span></span> <span data-ttu-id="48be2-202">Work with [iWellnessNow support team](mailto:info@iwellnessnow.com) to add the users in the iWellnessNow platform.</span><span class="sxs-lookup"><span data-stu-id="48be2-202">Work with [iWellnessNow support team](mailto:info@iwellnessnow.com) to add the users in the iWellnessNow platform.</span></span> <span data-ttu-id="48be2-203">Users must be created and activated before you use single sign-on</span><span class="sxs-lookup"><span data-stu-id="48be2-203">Users must be created and activated before you use single sign-on</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="48be2-204">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="48be2-204">Assign the Azure AD test user</span></span>

<span data-ttu-id="48be2-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to iWellnessNow.</span><span class="sxs-lookup"><span data-stu-id="48be2-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to iWellnessNow.</span></span>

![Assign the user role][200] 

<span data-ttu-id="48be2-207">**To assign Britta Simon to iWellnessNow, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="48be2-207">**To assign Britta Simon to iWellnessNow, perform the following steps:**</span></span>

1. <span data-ttu-id="48be2-208">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="48be2-208">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="48be2-210">In the applications list, select **iWellnessNow**.</span><span class="sxs-lookup"><span data-stu-id="48be2-210">In the applications list, select **iWellnessNow**.</span></span>

    ![The iWellnessNow link in the Applications list](./media/iwellnessnow-tutorial/tutorial_iwellnessnow_app.png)  

1. <span data-ttu-id="48be2-212">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="48be2-212">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="48be2-214">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="48be2-214">Click **Add** button.</span></span> <span data-ttu-id="48be2-215">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="48be2-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="48be2-217">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="48be2-217">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="48be2-218">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="48be2-218">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="48be2-219">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="48be2-219">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="48be2-220">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="48be2-220">Test single sign-on</span></span>

<span data-ttu-id="48be2-221">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="48be2-221">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="48be2-222">When you click the iWellnessNow tile in the Access Panel, you should get automatically signed-on to your iWellnessNow application.</span><span class="sxs-lookup"><span data-stu-id="48be2-222">When you click the iWellnessNow tile in the Access Panel, you should get automatically signed-on to your iWellnessNow application.</span></span>
<span data-ttu-id="48be2-223">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="48be2-223">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="48be2-224">Additional resources</span><span class="sxs-lookup"><span data-stu-id="48be2-224">Additional resources</span></span>

* [<span data-ttu-id="48be2-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48be2-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="48be2-226">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="48be2-226">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/iwellnessnow-tutorial/tutorial_general_01.png
[2]: ./media/iwellnessnow-tutorial/tutorial_general_02.png
[3]: ./media/iwellnessnow-tutorial/tutorial_general_03.png
[4]: ./media/iwellnessnow-tutorial/tutorial_general_04.png

[100]: ./media/iwellnessnow-tutorial/tutorial_general_100.png

[200]: ./media/iwellnessnow-tutorial/tutorial_general_200.png
[201]: ./media/iwellnessnow-tutorial/tutorial_general_201.png
[202]: ./media/iwellnessnow-tutorial/tutorial_general_202.png
[203]: ./media/iwellnessnow-tutorial/tutorial_general_203.png

