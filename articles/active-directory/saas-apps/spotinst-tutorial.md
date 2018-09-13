---
title: 'Tutorial: Azure Active Directory integration with Spotinst | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Spotinst.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2f6dbd70-c2db-4ae9-99ee-976c3090d214
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2018
ms.author: jeedes
ms.openlocfilehash: 7edf1cbc5cc351e25a9ae7b319768376ea9968a3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868261"
---
# <a name="tutorial-azure-active-directory-integration-with-spotinst"></a><span data-ttu-id="631da-103">Tutorial: Azure Active Directory integration with Spotinst</span><span class="sxs-lookup"><span data-stu-id="631da-103">Tutorial: Azure Active Directory integration with Spotinst</span></span>

<span data-ttu-id="631da-104">In this tutorial, you learn how to integrate Spotinst with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="631da-104">In this tutorial, you learn how to integrate Spotinst with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="631da-105">Integrating Spotinst with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="631da-105">Integrating Spotinst with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="631da-106">You can control in Azure AD who has access to Spotinst.</span><span class="sxs-lookup"><span data-stu-id="631da-106">You can control in Azure AD who has access to Spotinst.</span></span>
- <span data-ttu-id="631da-107">You can enable your users to automatically get signed-on to Spotinst (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="631da-107">You can enable your users to automatically get signed-on to Spotinst (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="631da-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="631da-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="631da-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="631da-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="631da-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="631da-110">Prerequisites</span></span>

<span data-ttu-id="631da-111">To configure Azure AD integration with Spotinst, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="631da-111">To configure Azure AD integration with Spotinst, you need the following items:</span></span>

- <span data-ttu-id="631da-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="631da-112">An Azure AD subscription</span></span>
- <span data-ttu-id="631da-113">A Spotinst single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="631da-113">A Spotinst single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="631da-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="631da-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="631da-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="631da-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="631da-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="631da-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="631da-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="631da-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="631da-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="631da-118">Scenario description</span></span>
<span data-ttu-id="631da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="631da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="631da-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="631da-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="631da-121">Adding Spotinst from the gallery</span><span class="sxs-lookup"><span data-stu-id="631da-121">Adding Spotinst from the gallery</span></span>
2. <span data-ttu-id="631da-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="631da-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-spotinst-from-the-gallery"></a><span data-ttu-id="631da-123">Adding Spotinst from the gallery</span><span class="sxs-lookup"><span data-stu-id="631da-123">Adding Spotinst from the gallery</span></span>
<span data-ttu-id="631da-124">To configure the integration of Spotinst into Azure AD, you need to add Spotinst from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="631da-124">To configure the integration of Spotinst into Azure AD, you need to add Spotinst from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="631da-125">**To add Spotinst from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="631da-125">**To add Spotinst from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="631da-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="631da-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="631da-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="631da-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="631da-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="631da-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="631da-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="631da-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="631da-133">In the search box, type **Spotinst**, select **Spotinst** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="631da-133">In the search box, type **Spotinst**, select **Spotinst** from result panel then click **Add** button to add the application.</span></span>

    ![Spotinst in the results list](./media/spotinst-tutorial/tutorial_spotinst_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="631da-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="631da-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="631da-136">In this section, you configure and test Azure AD single sign-on with Spotinst based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="631da-136">In this section, you configure and test Azure AD single sign-on with Spotinst based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="631da-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Spotinst is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="631da-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Spotinst is to a user in Azure AD.</span></span> <span data-ttu-id="631da-138">In other words, a link relationship between an Azure AD user and the related user in Spotinst needs to be established.</span><span class="sxs-lookup"><span data-stu-id="631da-138">In other words, a link relationship between an Azure AD user and the related user in Spotinst needs to be established.</span></span>

<span data-ttu-id="631da-139">To configure and test Azure AD single sign-on with Spotinst, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="631da-139">To configure and test Azure AD single sign-on with Spotinst, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="631da-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="631da-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="631da-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="631da-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="631da-142">**[Create a Spotinst test user](#create-a-spotinst-test-user)** - to have a counterpart of Britta Simon in Spotinst that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="631da-142">**[Create a Spotinst test user](#create-a-spotinst-test-user)** - to have a counterpart of Britta Simon in Spotinst that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="631da-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="631da-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="631da-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="631da-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="631da-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="631da-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="631da-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Spotinst application.</span><span class="sxs-lookup"><span data-stu-id="631da-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Spotinst application.</span></span>

<span data-ttu-id="631da-147">**To configure Azure AD single sign-on with Spotinst, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="631da-147">**To configure Azure AD single sign-on with Spotinst, perform the following steps:**</span></span>

1. <span data-ttu-id="631da-148">In the Azure portal, on the **Spotinst** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="631da-148">In the Azure portal, on the **Spotinst** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="631da-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="631da-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/spotinst-tutorial/tutorial_spotinst_samlbase.png)

3. <span data-ttu-id="631da-152">On the **Spotinst Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span><span class="sxs-lookup"><span data-stu-id="631da-152">On the **Spotinst Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Spotinst Domain and URLs single sign-on information](./media/spotinst-tutorial/tutorial_spotinst_url1.png)

    <span data-ttu-id="631da-154">a.</span><span class="sxs-lookup"><span data-stu-id="631da-154">a.</span></span> <span data-ttu-id="631da-155">Check **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="631da-155">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="631da-156">b.</span><span class="sxs-lookup"><span data-stu-id="631da-156">b.</span></span> <span data-ttu-id="631da-157">In the **Relay State** textbox, type a value: `<ID>`</span><span class="sxs-lookup"><span data-stu-id="631da-157">In the **Relay State** textbox, type a value: `<ID>`</span></span>

    <span data-ttu-id="631da-158">c.</span><span class="sxs-lookup"><span data-stu-id="631da-158">c.</span></span> <span data-ttu-id="631da-159">If you wish to configure the application in **SP** initiated mode, in the **Sign on URL** textbox, type the URL: `https://console.spotinst.com`</span><span class="sxs-lookup"><span data-stu-id="631da-159">If you wish to configure the application in **SP** initiated mode, in the **Sign on URL** textbox, type the URL: `https://console.spotinst.com`</span></span>

    > [!NOTE]
    > <span data-ttu-id="631da-160">The Relay State value is not real.</span><span class="sxs-lookup"><span data-stu-id="631da-160">The Relay State value is not real.</span></span> <span data-ttu-id="631da-161">You will update the Relay State value with the actual Relay State value, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="631da-161">You will update the Relay State value with the actual Relay State value, which is explained later in the tutorial.</span></span>

4. <span data-ttu-id="631da-162">Spotinst application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="631da-162">Spotinst application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="631da-163">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="631da-163">Configure the following claims for this application.</span></span> <span data-ttu-id="631da-164">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="631da-164">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="631da-165">The following screenshot shows an example for it.</span><span class="sxs-lookup"><span data-stu-id="631da-165">The following screenshot shows an example for it.</span></span>

    ![Configure Single Sign-On](./media/spotinst-tutorial/tutorial_Spotinst_attribute.png)

5. <span data-ttu-id="631da-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="631da-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>

    | <span data-ttu-id="631da-168">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="631da-168">Attribute Name</span></span> | <span data-ttu-id="631da-169">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="631da-169">Attribute Value</span></span> |
    | ---------------| --------------- |
    | <span data-ttu-id="631da-170">Email</span><span class="sxs-lookup"><span data-stu-id="631da-170">Email</span></span> | <span data-ttu-id="631da-171">user.mail</span><span class="sxs-lookup"><span data-stu-id="631da-171">user.mail</span></span> |
    | <span data-ttu-id="631da-172">FirstName</span><span class="sxs-lookup"><span data-stu-id="631da-172">FirstName</span></span> | <span data-ttu-id="631da-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="631da-173">user.givenname</span></span> |
    | <span data-ttu-id="631da-174">LastName</span><span class="sxs-lookup"><span data-stu-id="631da-174">LastName</span></span> | <span data-ttu-id="631da-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="631da-175">user.surname</span></span> |
    
    <span data-ttu-id="631da-176">a.</span><span class="sxs-lookup"><span data-stu-id="631da-176">a.</span></span> <span data-ttu-id="631da-177">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="631da-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/spotinst-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/spotinst-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="631da-180">b.</span><span class="sxs-lookup"><span data-stu-id="631da-180">b.</span></span> <span data-ttu-id="631da-181">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="631da-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="631da-182">c.</span><span class="sxs-lookup"><span data-stu-id="631da-182">c.</span></span> <span data-ttu-id="631da-183">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="631da-183">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="631da-184">d.</span><span class="sxs-lookup"><span data-stu-id="631da-184">d.</span></span> <span data-ttu-id="631da-185">Leave the **Namespace** blank.</span><span class="sxs-lookup"><span data-stu-id="631da-185">Leave the **Namespace** blank.</span></span>

    <span data-ttu-id="631da-186">e.</span><span class="sxs-lookup"><span data-stu-id="631da-186">e.</span></span> <span data-ttu-id="631da-187">Click **Ok**</span><span class="sxs-lookup"><span data-stu-id="631da-187">Click **Ok**</span></span>

6. <span data-ttu-id="631da-188">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="631da-188">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/spotinst-tutorial/tutorial_spotinst_certificate.png) 

7. <span data-ttu-id="631da-190">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="631da-190">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/spotinst-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="631da-192">In a different web browser window, login to Spotinst as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="631da-192">In a different web browser window, login to Spotinst as a Security Administrator.</span></span>

9. <span data-ttu-id="631da-193">Click on the **user icon** on the top right side of the screen and click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="631da-193">Click on the **user icon** on the top right side of the screen and click **Settings**.</span></span>

    ![Spotinst settings](./media/spotinst-tutorial/tutorial_spotinst_settings.png)

10. <span data-ttu-id="631da-195">Click on the **SECURITY** tab on the top and then select **Identity Providers** and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="631da-195">Click on the **SECURITY** tab on the top and then select **Identity Providers** and perform the following steps:</span></span>

    ![Spotinst security](./media/spotinst-tutorial/tutorial_spotinst_security.png)

    <span data-ttu-id="631da-197">a.</span><span class="sxs-lookup"><span data-stu-id="631da-197">a.</span></span> <span data-ttu-id="631da-198">Copy the **Relay State** value for your instance and paste it in **Relay State** textbox in **Spotinst Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="631da-198">Copy the **Relay State** value for your instance and paste it in **Relay State** textbox in **Spotinst Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="631da-199">b.</span><span class="sxs-lookup"><span data-stu-id="631da-199">b.</span></span> <span data-ttu-id="631da-200">Click **BROWSE** to upload the metadata xml file that you have downloaded from Azure portal</span><span class="sxs-lookup"><span data-stu-id="631da-200">Click **BROWSE** to upload the metadata xml file that you have downloaded from Azure portal</span></span>

    <span data-ttu-id="631da-201">c.</span><span class="sxs-lookup"><span data-stu-id="631da-201">c.</span></span> <span data-ttu-id="631da-202">Click **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="631da-202">Click **SAVE**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="631da-203">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="631da-203">Create an Azure AD test user</span></span>

<span data-ttu-id="631da-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="631da-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="631da-206">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="631da-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="631da-207">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="631da-207">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/spotinst-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="631da-209">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="631da-209">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/spotinst-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="631da-211">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="631da-211">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/spotinst-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="631da-213">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="631da-213">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/spotinst-tutorial/create_aaduser_04.png)

    <span data-ttu-id="631da-215">a.</span><span class="sxs-lookup"><span data-stu-id="631da-215">a.</span></span> <span data-ttu-id="631da-216">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="631da-216">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="631da-217">b.</span><span class="sxs-lookup"><span data-stu-id="631da-217">b.</span></span> <span data-ttu-id="631da-218">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="631da-218">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="631da-219">c.</span><span class="sxs-lookup"><span data-stu-id="631da-219">c.</span></span> <span data-ttu-id="631da-220">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="631da-220">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="631da-221">d.</span><span class="sxs-lookup"><span data-stu-id="631da-221">d.</span></span> <span data-ttu-id="631da-222">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="631da-222">Click **Create**.</span></span>

### <a name="create-a-spotinst-test-user"></a><span data-ttu-id="631da-223">Create a Spotinst test user</span><span class="sxs-lookup"><span data-stu-id="631da-223">Create a Spotinst test user</span></span>

<span data-ttu-id="631da-224">The objective of this section is to create a user called Britta Simon in Spotinst.</span><span class="sxs-lookup"><span data-stu-id="631da-224">The objective of this section is to create a user called Britta Simon in Spotinst.</span></span>

1. <span data-ttu-id="631da-225">If you have configured the application in the **SP** intiated mode, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="631da-225">If you have configured the application in the **SP** intiated mode, perform the following steps:</span></span>

   <span data-ttu-id="631da-226">a.</span><span class="sxs-lookup"><span data-stu-id="631da-226">a.</span></span> <span data-ttu-id="631da-227">In a different web browser window, login to Spotinst as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="631da-227">In a different web browser window, login to Spotinst as a Security Administrator.</span></span>

   <span data-ttu-id="631da-228">b.</span><span class="sxs-lookup"><span data-stu-id="631da-228">b.</span></span> <span data-ttu-id="631da-229">Click on the **user icon** on the top right side of the screen and click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="631da-229">Click on the **user icon** on the top right side of the screen and click **Settings**.</span></span>

    ![Spotinst settings](./media/spotinst-tutorial/tutorial_spotinst_settings.png)

    <span data-ttu-id="631da-231">c.</span><span class="sxs-lookup"><span data-stu-id="631da-231">c.</span></span> <span data-ttu-id="631da-232">Click **Users** and select **ADD USER**.</span><span class="sxs-lookup"><span data-stu-id="631da-232">Click **Users** and select **ADD USER**.</span></span>

    ![Spotinst settings](./media/spotinst-tutorial/adduser1.png)

    <span data-ttu-id="631da-234">d.</span><span class="sxs-lookup"><span data-stu-id="631da-234">d.</span></span> <span data-ttu-id="631da-235">On the add user section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="631da-235">On the add user section, perform the following steps:</span></span>

    ![Spotinst settings](./media/spotinst-tutorial/adduser2.png)

    * <span data-ttu-id="631da-237">In the **Full Name** textbox, enter the full name of user like **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="631da-237">In the **Full Name** textbox, enter the full name of user like **BrittaSimon**.</span></span>

    * <span data-ttu-id="631da-238">In the **Email** textbox, enter the email address of the user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="631da-238">In the **Email** textbox, enter the email address of the user like **brittasimon@contoso.com**.</span></span>

    * <span data-ttu-id="631da-239">Select your organization-specific details for the **Organization Role, Account Role, and Accounts**.</span><span class="sxs-lookup"><span data-stu-id="631da-239">Select your organization-specific details for the **Organization Role, Account Role, and Accounts**.</span></span>

2. <span data-ttu-id="631da-240">If you have configured the application in the **IDP** intiated mode, There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="631da-240">If you have configured the application in the **IDP** intiated mode, There is no action item for you in this section.</span></span> <span data-ttu-id="631da-241">Spotinst supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="631da-241">Spotinst supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="631da-242">A new user is created during an attempt to access Spotinst if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="631da-242">A new user is created during an attempt to access Spotinst if it doesn't exist yet.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="631da-243">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="631da-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="631da-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Spotinst.</span><span class="sxs-lookup"><span data-stu-id="631da-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Spotinst.</span></span>

![Assign the user role][200] 

<span data-ttu-id="631da-246">**To assign Britta Simon to Spotinst, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="631da-246">**To assign Britta Simon to Spotinst, perform the following steps:**</span></span>

1. <span data-ttu-id="631da-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="631da-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="631da-249">In the applications list, select **Spotinst**.</span><span class="sxs-lookup"><span data-stu-id="631da-249">In the applications list, select **Spotinst**.</span></span>

    ![The Spotinst link in the Applications list](./media/spotinst-tutorial/tutorial_spotinst_app.png)  

3. <span data-ttu-id="631da-251">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="631da-251">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="631da-253">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="631da-253">Click **Add** button.</span></span> <span data-ttu-id="631da-254">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="631da-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="631da-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="631da-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="631da-257">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="631da-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="631da-258">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="631da-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="631da-259">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="631da-259">Test single sign-on</span></span>

<span data-ttu-id="631da-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="631da-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="631da-261">When you click the Spotinst tile in the Access Panel, you should get automatically signed-on to your Spotinst application.</span><span class="sxs-lookup"><span data-stu-id="631da-261">When you click the Spotinst tile in the Access Panel, you should get automatically signed-on to your Spotinst application.</span></span>
<span data-ttu-id="631da-262">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="631da-262">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="631da-263">Additional resources</span><span class="sxs-lookup"><span data-stu-id="631da-263">Additional resources</span></span>

* [<span data-ttu-id="631da-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="631da-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="631da-265">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="631da-265">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/spotinst-tutorial/tutorial_general_01.png
[2]: ./media/spotinst-tutorial/tutorial_general_02.png
[3]: ./media/spotinst-tutorial/tutorial_general_03.png
[4]: ./media/spotinst-tutorial/tutorial_general_04.png

[100]: ./media/spotinst-tutorial/tutorial_general_100.png

[200]: ./media/spotinst-tutorial/tutorial_general_200.png
[201]: ./media/spotinst-tutorial/tutorial_general_201.png
[202]: ./media/spotinst-tutorial/tutorial_general_202.png
[203]: ./media/spotinst-tutorial/tutorial_general_203.png

