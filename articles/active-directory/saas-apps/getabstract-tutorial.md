---
title: 'Tutorial: Azure Active Directory integration with Getabstract | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Getabstract.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 2b63d048-b529-4fad-9e90-f244323409dd
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/15/2017
ms.author: jeedes
ms.openlocfilehash: 1bb43f65bd77315be398a9c22e7fc1500de07754
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857407"
---
# <a name="tutorial-azure-active-directory-integration-with-getabstract"></a><span data-ttu-id="d3ded-103">Tutorial: Azure Active Directory integration with Getabstract</span><span class="sxs-lookup"><span data-stu-id="d3ded-103">Tutorial: Azure Active Directory integration with Getabstract</span></span>

<span data-ttu-id="d3ded-104">In this tutorial, you learn how to integrate Getabstract with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d3ded-104">In this tutorial, you learn how to integrate Getabstract with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d3ded-105">Integrating Getabstract with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d3ded-105">Integrating Getabstract with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d3ded-106">You can control in Azure AD who has access to Getabstract.</span><span class="sxs-lookup"><span data-stu-id="d3ded-106">You can control in Azure AD who has access to Getabstract.</span></span>
- <span data-ttu-id="d3ded-107">You can enable your users to automatically get signed-on to Getabstract (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="d3ded-107">You can enable your users to automatically get signed-on to Getabstract (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d3ded-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d3ded-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="d3ded-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="d3ded-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3ded-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d3ded-110">Prerequisites</span></span>

<span data-ttu-id="d3ded-111">To configure Azure AD integration with Getabstract, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d3ded-111">To configure Azure AD integration with Getabstract, you need the following items:</span></span>

- <span data-ttu-id="d3ded-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d3ded-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d3ded-113">A Getabstract single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d3ded-113">A Getabstract single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d3ded-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d3ded-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d3ded-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d3ded-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d3ded-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="d3ded-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d3ded-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d3ded-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d3ded-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="d3ded-118">Scenario description</span></span>
<span data-ttu-id="d3ded-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d3ded-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d3ded-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d3ded-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d3ded-121">Adding Getabstract from the gallery</span><span class="sxs-lookup"><span data-stu-id="d3ded-121">Adding Getabstract from the gallery</span></span>
1. <span data-ttu-id="d3ded-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d3ded-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-getabstract-from-the-gallery"></a><span data-ttu-id="d3ded-123">Adding Getabstract from the gallery</span><span class="sxs-lookup"><span data-stu-id="d3ded-123">Adding Getabstract from the gallery</span></span>
<span data-ttu-id="d3ded-124">To configure the integration of Getabstract into Azure AD, you need to add Getabstract from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d3ded-124">To configure the integration of Getabstract into Azure AD, you need to add Getabstract from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d3ded-125">**To add Getabstract from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d3ded-125">**To add Getabstract from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d3ded-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d3ded-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="d3ded-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="d3ded-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d3ded-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d3ded-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="d3ded-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="d3ded-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="d3ded-133">In the search box, type **Getabstract**, select **Getabstract** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="d3ded-133">In the search box, type **Getabstract**, select **Getabstract** from result panel then click **Add** button to add the application.</span></span>

    ![Getabstract in the results list](./media/getabstract-tutorial/tutorial_getabstract_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d3ded-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d3ded-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d3ded-136">In this section, you configure and test Azure AD single sign-on with Getabstract based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d3ded-136">In this section, you configure and test Azure AD single sign-on with Getabstract based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d3ded-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Getabstract is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3ded-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Getabstract is to a user in Azure AD.</span></span> <span data-ttu-id="d3ded-138">In other words, a link relationship between an Azure AD user and the related user in Getabstract needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d3ded-138">In other words, a link relationship between an Azure AD user and the related user in Getabstract needs to be established.</span></span>

<span data-ttu-id="d3ded-139">In Getabstract, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="d3ded-139">In Getabstract, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d3ded-140">To configure and test Azure AD single sign-on with Getabstract, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d3ded-140">To configure and test Azure AD single sign-on with Getabstract, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d3ded-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d3ded-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="d3ded-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3ded-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="d3ded-143">**[Create a Getabstract test user](#create-a-getabstract-test-user)** - to have a counterpart of Britta Simon in Getabstract that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="d3ded-143">**[Create a Getabstract test user](#create-a-getabstract-test-user)** - to have a counterpart of Britta Simon in Getabstract that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="d3ded-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d3ded-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="d3ded-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d3ded-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d3ded-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d3ded-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d3ded-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Getabstract application.</span><span class="sxs-lookup"><span data-stu-id="d3ded-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Getabstract application.</span></span>

<span data-ttu-id="d3ded-148">**To configure Azure AD single sign-on with Getabstract, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d3ded-148">**To configure Azure AD single sign-on with Getabstract, perform the following steps:**</span></span>

1. <span data-ttu-id="d3ded-149">In the Azure portal, on the **Getabstract** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d3ded-149">In the Azure portal, on the **Getabstract** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="d3ded-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d3ded-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/getabstract-tutorial/tutorial_getabstract_samlbase.png)

1. <span data-ttu-id="d3ded-153">On the **Getabstract Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="d3ded-153">On the **Getabstract Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Getabstract Domain and URLs single sign-on information](./media/getabstract-tutorial/tutorial_getabstract_url.png)

    <span data-ttu-id="d3ded-155">a.</span><span class="sxs-lookup"><span data-stu-id="d3ded-155">a.</span></span> <span data-ttu-id="d3ded-156">In the **Identifier** textbox, type the URL:</span><span class="sxs-lookup"><span data-stu-id="d3ded-156">In the **Identifier** textbox, type the URL:</span></span>

    <span data-ttu-id="d3ded-157">For Stage/pre_production: `https://int.getabstract.com`</span><span class="sxs-lookup"><span data-stu-id="d3ded-157">For Stage/pre_production: `https://int.getabstract.com`</span></span>

    <span data-ttu-id="d3ded-158">For Production: `https://www.getabstract.com`</span><span class="sxs-lookup"><span data-stu-id="d3ded-158">For Production: `https://www.getabstract.com`</span></span>

    <span data-ttu-id="d3ded-159">b.</span><span class="sxs-lookup"><span data-stu-id="d3ded-159">b.</span></span> <span data-ttu-id="d3ded-160">In the **Reply URL** textbox, type the URL:</span><span class="sxs-lookup"><span data-stu-id="d3ded-160">In the **Reply URL** textbox, type the URL:</span></span>
    
    <span data-ttu-id="d3ded-161">For Stage/pre_production: `https://int.getabstract.com/ACS.do`</span><span class="sxs-lookup"><span data-stu-id="d3ded-161">For Stage/pre_production: `https://int.getabstract.com/ACS.do`</span></span>
    
    <span data-ttu-id="d3ded-162">For Production: `https://www.getabstract.com/ACS.do`</span><span class="sxs-lookup"><span data-stu-id="d3ded-162">For Production: `https://www.getabstract.com/ACS.do`</span></span>

1. <span data-ttu-id="d3ded-163">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="d3ded-163">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Getabstract Domain and URLs single sign-on information](./media/getabstract-tutorial/tutorial_getabstract_url1.png)

    <span data-ttu-id="d3ded-165">In the **Sign-on URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="d3ded-165">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    
    <span data-ttu-id="d3ded-166">For Stage/pre_production: `https://int.getabstract.com/portal/<org_username>`</span><span class="sxs-lookup"><span data-stu-id="d3ded-166">For Stage/pre_production: `https://int.getabstract.com/portal/<org_username>`</span></span>
    
    <span data-ttu-id="d3ded-167">For Production: `https://www.getabstract.com/portal/<org_username>`</span><span class="sxs-lookup"><span data-stu-id="d3ded-167">For Production: `https://www.getabstract.com/portal/<org_username>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d3ded-168">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="d3ded-168">This value is not real.</span></span> <span data-ttu-id="d3ded-169">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="d3ded-169">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="d3ded-170">Contact [Getabstract Client support team](https://www.getabstract.com/en/contact) to get this value.</span><span class="sxs-lookup"><span data-stu-id="d3ded-170">Contact [Getabstract Client support team](https://www.getabstract.com/en/contact) to get this value.</span></span>

1. <span data-ttu-id="d3ded-171">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d3ded-171">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/getabstract-tutorial/tutorial_getabstract_certificate.png) 

1. <span data-ttu-id="d3ded-173">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="d3ded-173">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/getabstract-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="d3ded-175">To configure single sign-on on **Getabstract** side, you need to send the downloaded **Metadata XML** to [Getabstract support team](https://www.getabstract.com/en/contact).</span><span class="sxs-lookup"><span data-stu-id="d3ded-175">To configure single sign-on on **Getabstract** side, you need to send the downloaded **Metadata XML** to [Getabstract support team](https://www.getabstract.com/en/contact).</span></span> <span data-ttu-id="d3ded-176">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="d3ded-176">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d3ded-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="d3ded-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d3ded-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="d3ded-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d3ded-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d3ded-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d3ded-180">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d3ded-180">Create an Azure AD test user</span></span>

<span data-ttu-id="d3ded-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3ded-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="d3ded-183">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d3ded-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d3ded-184">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="d3ded-184">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/getabstract-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="d3ded-186">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="d3ded-186">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/getabstract-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="d3ded-188">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="d3ded-188">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/getabstract-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="d3ded-190">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d3ded-190">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/getabstract-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d3ded-192">a.</span><span class="sxs-lookup"><span data-stu-id="d3ded-192">a.</span></span> <span data-ttu-id="d3ded-193">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d3ded-193">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d3ded-194">b.</span><span class="sxs-lookup"><span data-stu-id="d3ded-194">b.</span></span> <span data-ttu-id="d3ded-195">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3ded-195">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="d3ded-196">c.</span><span class="sxs-lookup"><span data-stu-id="d3ded-196">c.</span></span> <span data-ttu-id="d3ded-197">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="d3ded-197">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="d3ded-198">d.</span><span class="sxs-lookup"><span data-stu-id="d3ded-198">d.</span></span> <span data-ttu-id="d3ded-199">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d3ded-199">Click **Create**.</span></span>
 
### <a name="create-a-getabstract-test-user"></a><span data-ttu-id="d3ded-200">Create a Getabstract test user</span><span class="sxs-lookup"><span data-stu-id="d3ded-200">Create a Getabstract test user</span></span>

<span data-ttu-id="d3ded-201">The objective of this section is to create a user called Britta Simon in Getabstract.</span><span class="sxs-lookup"><span data-stu-id="d3ded-201">The objective of this section is to create a user called Britta Simon in Getabstract.</span></span> <span data-ttu-id="d3ded-202">Getabstract supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="d3ded-202">Getabstract supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="d3ded-203">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="d3ded-203">There is no action item for you in this section.</span></span> <span data-ttu-id="d3ded-204">A new user is created during an attempt to access Getabstract if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="d3ded-204">A new user is created during an attempt to access Getabstract if it doesn't exist yet.</span></span>
>[!Note]
><span data-ttu-id="d3ded-205">If you need to create a user manually, Contact [Getabstract support team](https://www.getabstract.com/en/contact)</span><span class="sxs-lookup"><span data-stu-id="d3ded-205">If you need to create a user manually, Contact [Getabstract support team](https://www.getabstract.com/en/contact)</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d3ded-206">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d3ded-206">Assign the Azure AD test user</span></span>

<span data-ttu-id="d3ded-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Getabstract.</span><span class="sxs-lookup"><span data-stu-id="d3ded-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Getabstract.</span></span>

![Assign the user role][200] 

<span data-ttu-id="d3ded-209">**To assign Britta Simon to Getabstract, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d3ded-209">**To assign Britta Simon to Getabstract, perform the following steps:**</span></span>

1. <span data-ttu-id="d3ded-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d3ded-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="d3ded-212">In the applications list, select **Getabstract**.</span><span class="sxs-lookup"><span data-stu-id="d3ded-212">In the applications list, select **Getabstract**.</span></span>

    ![The Getabstract link in the Applications list](./media/getabstract-tutorial/tutorial_getabstract_app.png)  

1. <span data-ttu-id="d3ded-214">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d3ded-214">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="d3ded-216">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="d3ded-216">Click **Add** button.</span></span> <span data-ttu-id="d3ded-217">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d3ded-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="d3ded-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="d3ded-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="d3ded-220">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="d3ded-220">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="d3ded-221">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d3ded-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d3ded-222">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="d3ded-222">Test single sign-on</span></span>

<span data-ttu-id="d3ded-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d3ded-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d3ded-224">When you click the Getabstract tile in the Access Panel, you should get automatically signed-on to your Getabstract application.</span><span class="sxs-lookup"><span data-stu-id="d3ded-224">When you click the Getabstract tile in the Access Panel, you should get automatically signed-on to your Getabstract application.</span></span>
<span data-ttu-id="d3ded-225">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d3ded-225">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d3ded-226">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d3ded-226">Additional resources</span></span>

* [<span data-ttu-id="d3ded-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d3ded-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="d3ded-228">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d3ded-228">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/getabstract-tutorial/tutorial_general_01.png
[2]: ./media/getabstract-tutorial/tutorial_general_02.png
[3]: ./media/getabstract-tutorial/tutorial_general_03.png
[4]: ./media/getabstract-tutorial/tutorial_general_04.png

[100]: ./media/getabstract-tutorial/tutorial_general_100.png

[200]: ./media/getabstract-tutorial/tutorial_general_200.png
[201]: ./media/getabstract-tutorial/tutorial_general_201.png
[202]: ./media/getabstract-tutorial/tutorial_general_202.png
[203]: ./media/getabstract-tutorial/tutorial_general_203.png

