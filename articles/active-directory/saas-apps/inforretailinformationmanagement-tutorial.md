---
title: 'Tutorial: Azure Active Directory integration with Infor Retail – Information Management | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Infor Retail – Information Management.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 5ff49168-ef81-4169-8e5e-dc86e24dd5e5
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 8676ae32de72a52f88d212d225610053b7ee5c4c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868714"
---
# <a name="tutorial-azure-active-directory-integration-with-infor-retail--information-management"></a><span data-ttu-id="4fe90-103">Tutorial: Azure Active Directory integration with Infor Retail – Information Management</span><span class="sxs-lookup"><span data-stu-id="4fe90-103">Tutorial: Azure Active Directory integration with Infor Retail – Information Management</span></span>

<span data-ttu-id="4fe90-104">In this tutorial, you learn how to integrate Infor Retail – Information Management with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4fe90-104">In this tutorial, you learn how to integrate Infor Retail – Information Management with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4fe90-105">Integrating Infor Retail – Information Management with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4fe90-105">Integrating Infor Retail – Information Management with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4fe90-106">You can control in Azure AD who has access to Infor Retail – Information Management.</span><span class="sxs-lookup"><span data-stu-id="4fe90-106">You can control in Azure AD who has access to Infor Retail – Information Management.</span></span>
- <span data-ttu-id="4fe90-107">You can enable your users to automatically get signed-on to Infor Retail – Information Management (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="4fe90-107">You can enable your users to automatically get signed-on to Infor Retail – Information Management (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4fe90-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4fe90-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="4fe90-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="4fe90-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fe90-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4fe90-110">Prerequisites</span></span>

<span data-ttu-id="4fe90-111">To configure Azure AD integration with Infor Retail – Information Management, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4fe90-111">To configure Azure AD integration with Infor Retail – Information Management, you need the following items:</span></span>

- <span data-ttu-id="4fe90-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4fe90-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4fe90-113">An Infor Retail – Information Management single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4fe90-113">An Infor Retail – Information Management single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4fe90-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4fe90-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4fe90-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4fe90-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4fe90-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="4fe90-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4fe90-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4fe90-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4fe90-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="4fe90-118">Scenario description</span></span>
<span data-ttu-id="4fe90-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4fe90-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4fe90-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4fe90-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4fe90-121">Adding Infor Retail – Information Management from the gallery</span><span class="sxs-lookup"><span data-stu-id="4fe90-121">Adding Infor Retail – Information Management from the gallery</span></span>
1. <span data-ttu-id="4fe90-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4fe90-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-infor-retail--information-management-from-the-gallery"></a><span data-ttu-id="4fe90-123">Adding Infor Retail – Information Management from the gallery</span><span class="sxs-lookup"><span data-stu-id="4fe90-123">Adding Infor Retail – Information Management from the gallery</span></span>
<span data-ttu-id="4fe90-124">To configure the integration of Infor Retail – Information Management into Azure AD, you need to add Infor Retail – Information Management from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4fe90-124">To configure the integration of Infor Retail – Information Management into Azure AD, you need to add Infor Retail – Information Management from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4fe90-125">**To add Infor Retail – Information Management from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4fe90-125">**To add Infor Retail – Information Management from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4fe90-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4fe90-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="4fe90-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="4fe90-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4fe90-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4fe90-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="4fe90-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="4fe90-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="4fe90-133">In the search box, type **Infor Retail – Information Management**, select **Infor Retail – Information Management** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="4fe90-133">In the search box, type **Infor Retail – Information Management**, select **Infor Retail – Information Management** from result panel then click **Add** button to add the application.</span></span>

    ![Infor Retail – Information Management in the results list](./media/inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4fe90-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4fe90-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4fe90-136">In this section, you configure and test Azure AD single sign-on with Infor Retail – Information Management based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4fe90-136">In this section, you configure and test Azure AD single sign-on with Infor Retail – Information Management based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4fe90-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Infor Retail – Information Management is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4fe90-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Infor Retail – Information Management is to a user in Azure AD.</span></span> <span data-ttu-id="4fe90-138">In other words, a link relationship between an Azure AD user and the related user in Infor Retail – Information Management needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4fe90-138">In other words, a link relationship between an Azure AD user and the related user in Infor Retail – Information Management needs to be established.</span></span>

<span data-ttu-id="4fe90-139">In Infor Retail – Information Management, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="4fe90-139">In Infor Retail – Information Management, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4fe90-140">To configure and test Azure AD single sign-on with Infor Retail – Information Management, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4fe90-140">To configure and test Azure AD single sign-on with Infor Retail – Information Management, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4fe90-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4fe90-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="4fe90-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4fe90-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="4fe90-143">**[Create an Infor Retail – Information Management test user](#create-an-infor-retail--information-management-test-user)** - to have a counterpart of Britta Simon in Infor Retail – Information Management that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="4fe90-143">**[Create an Infor Retail – Information Management test user](#create-an-infor-retail--information-management-test-user)** - to have a counterpart of Britta Simon in Infor Retail – Information Management that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="4fe90-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4fe90-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="4fe90-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4fe90-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4fe90-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4fe90-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4fe90-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Infor Retail – Information Management application.</span><span class="sxs-lookup"><span data-stu-id="4fe90-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Infor Retail – Information Management application.</span></span>

<span data-ttu-id="4fe90-148">**To configure Azure AD single sign-on with Infor Retail – Information Management, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4fe90-148">**To configure Azure AD single sign-on with Infor Retail – Information Management, perform the following steps:**</span></span>

1. <span data-ttu-id="4fe90-149">In the Azure portal, on the **Infor Retail – Information Management** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4fe90-149">In the Azure portal, on the **Infor Retail – Information Management** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="4fe90-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4fe90-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_samlbase.png)

1. <span data-ttu-id="4fe90-153">On the **Infor Retail – Information Management Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span><span class="sxs-lookup"><span data-stu-id="4fe90-153">On the **Infor Retail – Information Management Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Infor Retail – Information Management Domain and URLs single sign-on information IDP](./media/inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_url.png)

    <span data-ttu-id="4fe90-155">a.</span><span class="sxs-lookup"><span data-stu-id="4fe90-155">a.</span></span> <span data-ttu-id="4fe90-156">In the **Identifier** textbox, type a URL using the following patterns:</span><span class="sxs-lookup"><span data-stu-id="4fe90-156">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
    |   |
    | -- |
    | `https://<company name>.mingle.infor.com` |
    | `http://<company name>.mingledev.infor.com` |

    <span data-ttu-id="4fe90-157">b.</span><span class="sxs-lookup"><span data-stu-id="4fe90-157">b.</span></span> <span data-ttu-id="4fe90-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.mingle.infor.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="4fe90-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.mingle.infor.com/sp/ACS.saml2`</span></span>

1. <span data-ttu-id="4fe90-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="4fe90-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Infor Retail – Information Management Domain and URLs single sign-on information SP](./media/inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_url1.png)

    <span data-ttu-id="4fe90-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.mingle.infor.com/<company code>`</span><span class="sxs-lookup"><span data-stu-id="4fe90-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.mingle.infor.com/<company code>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="4fe90-162">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="4fe90-162">These values are not real.</span></span> <span data-ttu-id="4fe90-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="4fe90-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="4fe90-164">Contact [Infor Retail – Information Management Client support team](mailto:innovate@infor.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="4fe90-164">Contact [Infor Retail – Information Management Client support team](mailto:innovate@infor.com) to get these values.</span></span> 

1. <span data-ttu-id="4fe90-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4fe90-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_certificate.png) 

1. <span data-ttu-id="4fe90-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4fe90-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/inforretailinformationmanagement-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="4fe90-169">To configure single sign-on on **Infor Retail – Information Management** side, you need to send the downloaded **Metadata XML** to [Infor Retail – Information Management support team](mailto:innovate@infor.com).</span><span class="sxs-lookup"><span data-stu-id="4fe90-169">To configure single sign-on on **Infor Retail – Information Management** side, you need to send the downloaded **Metadata XML** to [Infor Retail – Information Management support team](mailto:innovate@infor.com).</span></span> <span data-ttu-id="4fe90-170">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="4fe90-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="4fe90-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="4fe90-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4fe90-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="4fe90-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4fe90-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4fe90-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4fe90-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4fe90-174">Create an Azure AD test user</span></span>

<span data-ttu-id="4fe90-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4fe90-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="4fe90-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4fe90-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4fe90-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="4fe90-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/inforretailinformationmanagement-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="4fe90-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4fe90-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/inforretailinformationmanagement-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="4fe90-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="4fe90-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/inforretailinformationmanagement-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="4fe90-184">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4fe90-184">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/inforretailinformationmanagement-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4fe90-186">a.</span><span class="sxs-lookup"><span data-stu-id="4fe90-186">a.</span></span> <span data-ttu-id="4fe90-187">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4fe90-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4fe90-188">b.</span><span class="sxs-lookup"><span data-stu-id="4fe90-188">b.</span></span> <span data-ttu-id="4fe90-189">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4fe90-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="4fe90-190">c.</span><span class="sxs-lookup"><span data-stu-id="4fe90-190">c.</span></span> <span data-ttu-id="4fe90-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="4fe90-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="4fe90-192">d.</span><span class="sxs-lookup"><span data-stu-id="4fe90-192">d.</span></span> <span data-ttu-id="4fe90-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4fe90-193">Click **Create**.</span></span>
 
### <a name="create-an-infor-retail--information-management-test-user"></a><span data-ttu-id="4fe90-194">Create an Infor Retail – Information Management test user</span><span class="sxs-lookup"><span data-stu-id="4fe90-194">Create an Infor Retail – Information Management test user</span></span>

<span data-ttu-id="4fe90-195">In this section, you create a user called Britta Simon in Infor Retail – Information Management.</span><span class="sxs-lookup"><span data-stu-id="4fe90-195">In this section, you create a user called Britta Simon in Infor Retail – Information Management.</span></span> <span data-ttu-id="4fe90-196">Please work with [Infor Retail – Information Management support team](mailto:innovate@infor.com) to add the users in the Infor Retail – Information Management platform.</span><span class="sxs-lookup"><span data-stu-id="4fe90-196">Please work with [Infor Retail – Information Management support team](mailto:innovate@infor.com) to add the users in the Infor Retail – Information Management platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4fe90-197">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4fe90-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="4fe90-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Infor Retail – Information Management.</span><span class="sxs-lookup"><span data-stu-id="4fe90-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Infor Retail – Information Management.</span></span>

![Assign the user role][200] 

<span data-ttu-id="4fe90-200">**To assign Britta Simon to Infor Retail – Information Management, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4fe90-200">**To assign Britta Simon to Infor Retail – Information Management, perform the following steps:**</span></span>

1. <span data-ttu-id="4fe90-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4fe90-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="4fe90-203">In the applications list, select **Infor Retail – Information Management**.</span><span class="sxs-lookup"><span data-stu-id="4fe90-203">In the applications list, select **Infor Retail – Information Management**.</span></span>

    ![The Infor Retail – Information Management link in the Applications list](./media/inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_app.png)  

1. <span data-ttu-id="4fe90-205">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="4fe90-205">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="4fe90-207">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="4fe90-207">Click **Add** button.</span></span> <span data-ttu-id="4fe90-208">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4fe90-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="4fe90-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="4fe90-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="4fe90-211">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="4fe90-211">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="4fe90-212">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4fe90-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4fe90-213">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="4fe90-213">Test single sign-on</span></span>

<span data-ttu-id="4fe90-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4fe90-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4fe90-215">When you click the Infor Retail – Information Management tile in the Access Panel, you should get automatically signed-on to your Infor Retail – Information Management application.</span><span class="sxs-lookup"><span data-stu-id="4fe90-215">When you click the Infor Retail – Information Management tile in the Access Panel, you should get automatically signed-on to your Infor Retail – Information Management application.</span></span>
<span data-ttu-id="4fe90-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4fe90-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4fe90-217">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4fe90-217">Additional resources</span></span>

* [<span data-ttu-id="4fe90-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4fe90-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="4fe90-219">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4fe90-219">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/inforretailinformationmanagement-tutorial/tutorial_general_01.png
[2]: ./media/inforretailinformationmanagement-tutorial/tutorial_general_02.png
[3]: ./media/inforretailinformationmanagement-tutorial/tutorial_general_03.png
[4]: ./media/inforretailinformationmanagement-tutorial/tutorial_general_04.png

[100]: ./media/inforretailinformationmanagement-tutorial/tutorial_general_100.png

[200]: ./media/inforretailinformationmanagement-tutorial/tutorial_general_200.png
[201]: ./media/inforretailinformationmanagement-tutorial/tutorial_general_201.png
[202]: ./media/inforretailinformationmanagement-tutorial/tutorial_general_202.png
[203]: ./media/inforretailinformationmanagement-tutorial/tutorial_general_203.png

