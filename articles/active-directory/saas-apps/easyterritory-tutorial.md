---
title: 'Tutorial: Azure Active Directory integration with EasyTerritory | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and EasyTerritory.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: d29b362d-e986-4f67-8ff2-e158e49353aa
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 33389d7d9029a88cc72bce47d87c62233063c804
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857962"
---
# <a name="tutorial-azure-active-directory-integration-with-easyterritory"></a><span data-ttu-id="60356-103">Tutorial: Azure Active Directory integration with EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="60356-103">Tutorial: Azure Active Directory integration with EasyTerritory</span></span>

<span data-ttu-id="60356-104">In this tutorial, you learn how to integrate EasyTerritory with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="60356-104">In this tutorial, you learn how to integrate EasyTerritory with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="60356-105">Integrating EasyTerritory with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="60356-105">Integrating EasyTerritory with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="60356-106">You can control in Azure AD who has access to EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="60356-106">You can control in Azure AD who has access to EasyTerritory.</span></span>
- <span data-ttu-id="60356-107">You can enable your users to automatically get signed-on to EasyTerritory (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="60356-107">You can enable your users to automatically get signed-on to EasyTerritory (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="60356-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="60356-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="60356-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="60356-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60356-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="60356-110">Prerequisites</span></span>

<span data-ttu-id="60356-111">To configure Azure AD integration with EasyTerritory, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="60356-111">To configure Azure AD integration with EasyTerritory, you need the following items:</span></span>

- <span data-ttu-id="60356-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="60356-112">An Azure AD subscription</span></span>
- <span data-ttu-id="60356-113">A EasyTerritory single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="60356-113">A EasyTerritory single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="60356-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="60356-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="60356-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="60356-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="60356-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="60356-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="60356-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="60356-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="60356-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="60356-118">Scenario description</span></span>
<span data-ttu-id="60356-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="60356-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="60356-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="60356-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="60356-121">Adding EasyTerritory from the gallery</span><span class="sxs-lookup"><span data-stu-id="60356-121">Adding EasyTerritory from the gallery</span></span>
1. <span data-ttu-id="60356-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="60356-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-easyterritory-from-the-gallery"></a><span data-ttu-id="60356-123">Adding EasyTerritory from the gallery</span><span class="sxs-lookup"><span data-stu-id="60356-123">Adding EasyTerritory from the gallery</span></span>
<span data-ttu-id="60356-124">To configure the integration of EasyTerritory into Azure AD, you need to add EasyTerritory from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="60356-124">To configure the integration of EasyTerritory into Azure AD, you need to add EasyTerritory from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="60356-125">**To add EasyTerritory from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="60356-125">**To add EasyTerritory from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="60356-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="60356-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="60356-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="60356-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="60356-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="60356-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="60356-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="60356-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="60356-133">In the search box, type **EasyTerritory**, select **EasyTerritory** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="60356-133">In the search box, type **EasyTerritory**, select **EasyTerritory** from result panel then click **Add** button to add the application.</span></span>

    ![EasyTerritory in the results list](./media/easyterritory-tutorial/tutorial_easyterritory_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="60356-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="60356-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="60356-136">In this section, you configure and test Azure AD single sign-on with EasyTerritory based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="60356-136">In this section, you configure and test Azure AD single sign-on with EasyTerritory based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="60356-137">For single sign-on to work, Azure AD needs to know what the counterpart user in EasyTerritory is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60356-137">For single sign-on to work, Azure AD needs to know what the counterpart user in EasyTerritory is to a user in Azure AD.</span></span> <span data-ttu-id="60356-138">In other words, a link relationship between an Azure AD user and the related user in EasyTerritory needs to be established.</span><span class="sxs-lookup"><span data-stu-id="60356-138">In other words, a link relationship between an Azure AD user and the related user in EasyTerritory needs to be established.</span></span>

<span data-ttu-id="60356-139">In EasyTerritory, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="60356-139">In EasyTerritory, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="60356-140">To configure and test Azure AD single sign-on with EasyTerritory, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="60356-140">To configure and test Azure AD single sign-on with EasyTerritory, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="60356-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="60356-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="60356-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="60356-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="60356-143">**[Create a EasyTerritory test user](#create-a-easyterritory-test-user)** - to have a counterpart of Britta Simon in EasyTerritory that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="60356-143">**[Create a EasyTerritory test user](#create-a-easyterritory-test-user)** - to have a counterpart of Britta Simon in EasyTerritory that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="60356-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="60356-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="60356-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="60356-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="60356-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="60356-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="60356-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EasyTerritory application.</span><span class="sxs-lookup"><span data-stu-id="60356-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EasyTerritory application.</span></span>

<span data-ttu-id="60356-148">**To configure Azure AD single sign-on with EasyTerritory, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="60356-148">**To configure Azure AD single sign-on with EasyTerritory, perform the following steps:**</span></span>

1. <span data-ttu-id="60356-149">In the Azure portal, on the **EasyTerritory** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="60356-149">In the Azure portal, on the **EasyTerritory** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="60356-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="60356-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/easyterritory-tutorial/tutorial_easyterritory_samlbase.png)

1. <span data-ttu-id="60356-153">On the **EasyTerritory Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span><span class="sxs-lookup"><span data-stu-id="60356-153">On the **EasyTerritory Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![EasyTerritory Domain and URLs single sign-on information](./media/easyterritory-tutorial/tutorial_easyterritory_url.png)

    <span data-ttu-id="60356-155">a.</span><span class="sxs-lookup"><span data-stu-id="60356-155">a.</span></span> <span data-ttu-id="60356-156">In the **Identifier** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/dev/`</span><span class="sxs-lookup"><span data-stu-id="60356-156">In the **Identifier** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/dev/`</span></span>

    <span data-ttu-id="60356-157">b.</span><span class="sxs-lookup"><span data-stu-id="60356-157">b.</span></span> <span data-ttu-id="60356-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`</span><span class="sxs-lookup"><span data-stu-id="60356-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`</span></span>

1. <span data-ttu-id="60356-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="60356-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![EasyTerritory Domain and URLs single sign-on information](./media/easyterritory-tutorial/tutorial_easyterritory_url1.png)

    <span data-ttu-id="60356-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.easyterritory.com/`</span><span class="sxs-lookup"><span data-stu-id="60356-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.easyterritory.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="60356-162">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="60356-162">These values are not real.</span></span> <span data-ttu-id="60356-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="60356-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="60356-164">Contact [EasyTerritory Client support team](mailto:sales@easyterritory.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="60356-164">Contact [EasyTerritory Client support team](mailto:sales@easyterritory.com) to get these values.</span></span> 

1. <span data-ttu-id="60356-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="60356-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/easyterritory-tutorial/tutorial_easyterritory_certificate.png) 

1. <span data-ttu-id="60356-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="60356-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/easyterritory-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="60356-169">To configure single sign-on on **EasyTerritory** side, you need to send the downloaded **Metadata XML** to [EasyTerritory support team](mailto:sales@easyterritory.com).</span><span class="sxs-lookup"><span data-stu-id="60356-169">To configure single sign-on on **EasyTerritory** side, you need to send the downloaded **Metadata XML** to [EasyTerritory support team](mailto:sales@easyterritory.com).</span></span> <span data-ttu-id="60356-170">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="60356-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="60356-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="60356-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="60356-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="60356-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="60356-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="60356-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="60356-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="60356-174">Create an Azure AD test user</span></span>

<span data-ttu-id="60356-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="60356-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="60356-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="60356-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="60356-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="60356-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/easyterritory-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="60356-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="60356-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/easyterritory-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="60356-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="60356-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/easyterritory-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="60356-184">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="60356-184">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/easyterritory-tutorial/create_aaduser_04.png)

    <span data-ttu-id="60356-186">a.</span><span class="sxs-lookup"><span data-stu-id="60356-186">a.</span></span> <span data-ttu-id="60356-187">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="60356-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="60356-188">b.</span><span class="sxs-lookup"><span data-stu-id="60356-188">b.</span></span> <span data-ttu-id="60356-189">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="60356-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="60356-190">c.</span><span class="sxs-lookup"><span data-stu-id="60356-190">c.</span></span> <span data-ttu-id="60356-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="60356-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="60356-192">d.</span><span class="sxs-lookup"><span data-stu-id="60356-192">d.</span></span> <span data-ttu-id="60356-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="60356-193">Click **Create**.</span></span>
 
### <a name="create-a-easyterritory-test-user"></a><span data-ttu-id="60356-194">Create a EasyTerritory test user</span><span class="sxs-lookup"><span data-stu-id="60356-194">Create a EasyTerritory test user</span></span>

<span data-ttu-id="60356-195">In this section, you create a user called Britta Simon in EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="60356-195">In this section, you create a user called Britta Simon in EasyTerritory.</span></span> <span data-ttu-id="60356-196">Please work with [EasyTerritory support team](mailto:sales@easyterritory.com) to add the users in the EasyTerritory platform.</span><span class="sxs-lookup"><span data-stu-id="60356-196">Please work with [EasyTerritory support team](mailto:sales@easyterritory.com) to add the users in the EasyTerritory platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="60356-197">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="60356-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="60356-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="60356-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EasyTerritory.</span></span>

![Assign the user role][200] 

<span data-ttu-id="60356-200">**To assign Britta Simon to EasyTerritory, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="60356-200">**To assign Britta Simon to EasyTerritory, perform the following steps:**</span></span>

1. <span data-ttu-id="60356-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="60356-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="60356-203">In the applications list, select **EasyTerritory**.</span><span class="sxs-lookup"><span data-stu-id="60356-203">In the applications list, select **EasyTerritory**.</span></span>

    ![The EasyTerritory link in the Applications list](./media/easyterritory-tutorial/tutorial_easyterritory_app.png)  

1. <span data-ttu-id="60356-205">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="60356-205">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="60356-207">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="60356-207">Click **Add** button.</span></span> <span data-ttu-id="60356-208">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="60356-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="60356-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="60356-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="60356-211">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="60356-211">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="60356-212">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="60356-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="60356-213">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="60356-213">Test single sign-on</span></span>

<span data-ttu-id="60356-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="60356-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="60356-215">When you click the EasyTerritory tile in the Access Panel, you should get automatically signed-on to your EasyTerritory application.</span><span class="sxs-lookup"><span data-stu-id="60356-215">When you click the EasyTerritory tile in the Access Panel, you should get automatically signed-on to your EasyTerritory application.</span></span>
<span data-ttu-id="60356-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="60356-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="60356-217">Additional resources</span><span class="sxs-lookup"><span data-stu-id="60356-217">Additional resources</span></span>

* [<span data-ttu-id="60356-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="60356-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="60356-219">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="60356-219">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)




<!--Image references-->

[1]: ./media/easyterritory-tutorial/tutorial_general_01.png
[2]: ./media/easyterritory-tutorial/tutorial_general_02.png
[3]: ./media/easyterritory-tutorial/tutorial_general_03.png
[4]: ./media/easyterritory-tutorial/tutorial_general_04.png

[100]: ./media/easyterritory-tutorial/tutorial_general_100.png

[200]: ./media/easyterritory-tutorial/tutorial_general_200.png
[201]: ./media/easyterritory-tutorial/tutorial_general_201.png
[202]: ./media/easyterritory-tutorial/tutorial_general_202.png
[203]: ./media/easyterritory-tutorial/tutorial_general_203.png

