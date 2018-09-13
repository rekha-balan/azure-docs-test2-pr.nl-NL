---
title: 'Tutorial: Azure Active Directory integration with SafetyNet | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SafetyNet.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: caa96ea2-da21-4529-8fab-0e06367beb40
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/16/2018
ms.author: jeedes
ms.openlocfilehash: 7756e943d25a02b3ec3e5a9150bb5eec8485eda7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866429"
---
# <a name="tutorial-azure-active-directory-integration-with-safetynet"></a><span data-ttu-id="0b6e1-103">Tutorial: Azure Active Directory integration with SafetyNet</span><span class="sxs-lookup"><span data-stu-id="0b6e1-103">Tutorial: Azure Active Directory integration with SafetyNet</span></span>

<span data-ttu-id="0b6e1-104">In this tutorial, you learn how to integrate SafetyNet with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0b6e1-104">In this tutorial, you learn how to integrate SafetyNet with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0b6e1-105">Integrating SafetyNet with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="0b6e1-105">Integrating SafetyNet with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0b6e1-106">You can control in Azure AD who has access to SafetyNet.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-106">You can control in Azure AD who has access to SafetyNet.</span></span>
- <span data-ttu-id="0b6e1-107">You can enable your users to automatically get signed-on to SafetyNet (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-107">You can enable your users to automatically get signed-on to SafetyNet (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0b6e1-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="0b6e1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="0b6e1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b6e1-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0b6e1-110">Prerequisites</span></span>

<span data-ttu-id="0b6e1-111">To configure Azure AD integration with SafetyNet, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="0b6e1-111">To configure Azure AD integration with SafetyNet, you need the following items:</span></span>

- <span data-ttu-id="0b6e1-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="0b6e1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0b6e1-113">A SafetyNet single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="0b6e1-113">A SafetyNet single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0b6e1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0b6e1-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="0b6e1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0b6e1-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0b6e1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0b6e1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0b6e1-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="0b6e1-118">Scenario description</span></span>
<span data-ttu-id="0b6e1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0b6e1-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="0b6e1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0b6e1-121">Adding SafetyNet from the gallery</span><span class="sxs-lookup"><span data-stu-id="0b6e1-121">Adding SafetyNet from the gallery</span></span>
1. <span data-ttu-id="0b6e1-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0b6e1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-safetynet-from-the-gallery"></a><span data-ttu-id="0b6e1-123">Adding SafetyNet from the gallery</span><span class="sxs-lookup"><span data-stu-id="0b6e1-123">Adding SafetyNet from the gallery</span></span>
<span data-ttu-id="0b6e1-124">To configure the integration of SafetyNet into Azure AD, you need to add SafetyNet from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-124">To configure the integration of SafetyNet into Azure AD, you need to add SafetyNet from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0b6e1-125">**To add SafetyNet from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0b6e1-125">**To add SafetyNet from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0b6e1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="0b6e1-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0b6e1-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="0b6e1-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="0b6e1-133">In the search box, type **SafetyNet**, select **SafetyNet** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-133">In the search box, type **SafetyNet**, select **SafetyNet** from result panel then click **Add** button to add the application.</span></span>

    ![SafetyNet in the results list](./media/safetynet-tutorial/tutorial_safetynet_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0b6e1-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0b6e1-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0b6e1-136">In this section, you configure and test Azure AD single sign-on with SafetyNet based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0b6e1-136">In this section, you configure and test Azure AD single sign-on with SafetyNet based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0b6e1-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SafetyNet is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SafetyNet is to a user in Azure AD.</span></span> <span data-ttu-id="0b6e1-138">In other words, a link relationship between an Azure AD user and the related user in SafetyNet needs to be established.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-138">In other words, a link relationship between an Azure AD user and the related user in SafetyNet needs to be established.</span></span>

<span data-ttu-id="0b6e1-139">To configure and test Azure AD single sign-on with SafetyNet, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="0b6e1-139">To configure and test Azure AD single sign-on with SafetyNet, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0b6e1-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="0b6e1-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="0b6e1-142">**[Create a SafetyNet test user](#create-a-safetynet-test-user)** - to have a counterpart of Britta Simon in SafetyNet that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-142">**[Create a SafetyNet test user](#create-a-safetynet-test-user)** - to have a counterpart of Britta Simon in SafetyNet that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="0b6e1-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="0b6e1-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0b6e1-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0b6e1-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0b6e1-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SafetyNet application.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SafetyNet application.</span></span>

<span data-ttu-id="0b6e1-147">**To configure Azure AD single sign-on with SafetyNet, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0b6e1-147">**To configure Azure AD single sign-on with SafetyNet, perform the following steps:**</span></span>

1. <span data-ttu-id="0b6e1-148">In the Azure portal, on the **SafetyNet** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-148">In the Azure portal, on the **SafetyNet** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="0b6e1-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/safetynet-tutorial/tutorial_safetynet_samlbase.png)

1. <span data-ttu-id="0b6e1-152">On the **SafetyNet Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="0b6e1-152">On the **SafetyNet Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![SafetyNet Domain and URLs single sign-on information](./media/safetynet-tutorial/tutorial_safetynet_url.png)

    <span data-ttu-id="0b6e1-154">a.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-154">a.</span></span> <span data-ttu-id="0b6e1-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.predictivesolutions.com/sp`</span><span class="sxs-lookup"><span data-stu-id="0b6e1-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.predictivesolutions.com/sp`</span></span>

    <span data-ttu-id="0b6e1-156">b.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-156">b.</span></span> <span data-ttu-id="0b6e1-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.predictivesolutions.com/CRMApp/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="0b6e1-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.predictivesolutions.com/CRMApp/saml/SSO`</span></span>

1. <span data-ttu-id="0b6e1-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="0b6e1-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![SafetyNet Domain and URLs single sign-on information](./media/safetynet-tutorial/tutorial_safetynet_url1.png)

    <span data-ttu-id="0b6e1-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.predictivesolutions.com`</span><span class="sxs-lookup"><span data-stu-id="0b6e1-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.predictivesolutions.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="0b6e1-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-161">These values are not real.</span></span> <span data-ttu-id="0b6e1-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="0b6e1-163">Contact [SafetyNet Client support team](mailto:dev@predictivesolutions.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-163">Contact [SafetyNet Client support team](mailto:dev@predictivesolutions.com) to get these values.</span></span>

1. <span data-ttu-id="0b6e1-164">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-164">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

    ![The Certificate download link](./media/safetynet-tutorial/tutorial_safetynet_certificate.png)

1. <span data-ttu-id="0b6e1-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/safetynet-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="0b6e1-168">To configure single sign-on on **SafetyNet** side, you need to send the **App Federation Metadata Url** to [SafetyNet support team](mailto:dev@predictivesolutions.com).</span><span class="sxs-lookup"><span data-stu-id="0b6e1-168">To configure single sign-on on **SafetyNet** side, you need to send the **App Federation Metadata Url** to [SafetyNet support team](mailto:dev@predictivesolutions.com).</span></span> <span data-ttu-id="0b6e1-169">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0b6e1-170">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0b6e1-170">Create an Azure AD test user</span></span>

<span data-ttu-id="0b6e1-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="0b6e1-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0b6e1-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0b6e1-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/safetynet-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="0b6e1-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/safetynet-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="0b6e1-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/safetynet-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="0b6e1-180">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0b6e1-180">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/safetynet-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0b6e1-182">a.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-182">a.</span></span> <span data-ttu-id="0b6e1-183">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0b6e1-184">b.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-184">b.</span></span> <span data-ttu-id="0b6e1-185">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="0b6e1-186">c.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-186">c.</span></span> <span data-ttu-id="0b6e1-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="0b6e1-188">d.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-188">d.</span></span> <span data-ttu-id="0b6e1-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-189">Click **Create**.</span></span>
 
### <a name="create-a-safetynet-test-user"></a><span data-ttu-id="0b6e1-190">Create a SafetyNet test user</span><span class="sxs-lookup"><span data-stu-id="0b6e1-190">Create a SafetyNet test user</span></span>

<span data-ttu-id="0b6e1-191">In this section, you create a user called Britta Simon in SafetyNet.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-191">In this section, you create a user called Britta Simon in SafetyNet.</span></span> <span data-ttu-id="0b6e1-192">Work with [SafetyNet support team](mailto:dev@predictivesolutions.com) to add the users in the SafetyNet platform.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-192">Work with [SafetyNet support team](mailto:dev@predictivesolutions.com) to add the users in the SafetyNet platform.</span></span> <span data-ttu-id="0b6e1-193">Users must be created and activated before you use single sign-on</span><span class="sxs-lookup"><span data-stu-id="0b6e1-193">Users must be created and activated before you use single sign-on</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0b6e1-194">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0b6e1-194">Assign the Azure AD test user</span></span>

<span data-ttu-id="0b6e1-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SafetyNet.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SafetyNet.</span></span>

![Assign the user role][200] 

<span data-ttu-id="0b6e1-197">**To assign Britta Simon to SafetyNet, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0b6e1-197">**To assign Britta Simon to SafetyNet, perform the following steps:**</span></span>

1. <span data-ttu-id="0b6e1-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="0b6e1-200">In the applications list, select **SafetyNet**.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-200">In the applications list, select **SafetyNet**.</span></span>

    ![The SafetyNet link in the Applications list](./media/safetynet-tutorial/tutorial_safetynet_app.png)  

1. <span data-ttu-id="0b6e1-202">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-202">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="0b6e1-204">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-204">Click **Add** button.</span></span> <span data-ttu-id="0b6e1-205">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="0b6e1-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="0b6e1-208">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-208">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="0b6e1-209">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0b6e1-210">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="0b6e1-210">Test single sign-on</span></span>

<span data-ttu-id="0b6e1-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0b6e1-212">When you click the SafetyNet tile in the Access Panel, you should get automatically signed-on to your SafetyNet application.</span><span class="sxs-lookup"><span data-stu-id="0b6e1-212">When you click the SafetyNet tile in the Access Panel, you should get automatically signed-on to your SafetyNet application.</span></span>
<span data-ttu-id="0b6e1-213">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0b6e1-213">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0b6e1-214">Additional resources</span><span class="sxs-lookup"><span data-stu-id="0b6e1-214">Additional resources</span></span>

* [<span data-ttu-id="0b6e1-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0b6e1-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="0b6e1-216">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0b6e1-216">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/safetynet-tutorial/tutorial_general_01.png
[2]: ./media/safetynet-tutorial/tutorial_general_02.png
[3]: ./media/safetynet-tutorial/tutorial_general_03.png
[4]: ./media/safetynet-tutorial/tutorial_general_04.png

[100]: ./media/safetynet-tutorial/tutorial_general_100.png

[200]: ./media/safetynet-tutorial/tutorial_general_200.png
[201]: ./media/safetynet-tutorial/tutorial_general_201.png
[202]: ./media/safetynet-tutorial/tutorial_general_202.png
[203]: ./media/safetynet-tutorial/tutorial_general_203.png

