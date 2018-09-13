---
title: 'Tutorial: Azure Active Directory integration with TurboRater | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and TurboRater.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: abb116b8-8024-4cc6-bc81-f32ef490ea17
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2017
ms.author: jeedes
ms.openlocfilehash: 3dfa824d680f7014ee63b8c83d26dc29d42c7fe9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870683"
---
# <a name="tutorial-azure-active-directory-integration-with-turborater"></a><span data-ttu-id="3cef9-103">Tutorial: Azure Active Directory integration with TurboRater</span><span class="sxs-lookup"><span data-stu-id="3cef9-103">Tutorial: Azure Active Directory integration with TurboRater</span></span>

<span data-ttu-id="3cef9-104">In this tutorial, you learn how to integrate TurboRater with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3cef9-104">In this tutorial, you learn how to integrate TurboRater with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3cef9-105">Integrating TurboRater with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3cef9-105">Integrating TurboRater with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3cef9-106">You can control in Azure AD who has access to TurboRater.</span><span class="sxs-lookup"><span data-stu-id="3cef9-106">You can control in Azure AD who has access to TurboRater.</span></span>
- <span data-ttu-id="3cef9-107">You can enable your users to automatically get signed-on to TurboRater (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="3cef9-107">You can enable your users to automatically get signed-on to TurboRater (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3cef9-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3cef9-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="3cef9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="3cef9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cef9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3cef9-110">Prerequisites</span></span>

<span data-ttu-id="3cef9-111">To configure Azure AD integration with TurboRater, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="3cef9-111">To configure Azure AD integration with TurboRater, you need the following items:</span></span>

- <span data-ttu-id="3cef9-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="3cef9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3cef9-113">A TurboRater single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="3cef9-113">A TurboRater single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3cef9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="3cef9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3cef9-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="3cef9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3cef9-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="3cef9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3cef9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3cef9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3cef9-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="3cef9-118">Scenario description</span></span>
<span data-ttu-id="3cef9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="3cef9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3cef9-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="3cef9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3cef9-121">Adding TurboRater from the gallery</span><span class="sxs-lookup"><span data-stu-id="3cef9-121">Adding TurboRater from the gallery</span></span>
1. <span data-ttu-id="3cef9-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3cef9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-turborater-from-the-gallery"></a><span data-ttu-id="3cef9-123">Adding TurboRater from the gallery</span><span class="sxs-lookup"><span data-stu-id="3cef9-123">Adding TurboRater from the gallery</span></span>
<span data-ttu-id="3cef9-124">To configure the integration of TurboRater into Azure AD, you need to add TurboRater from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="3cef9-124">To configure the integration of TurboRater into Azure AD, you need to add TurboRater from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3cef9-125">**To add TurboRater from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3cef9-125">**To add TurboRater from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3cef9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="3cef9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="3cef9-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="3cef9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3cef9-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3cef9-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="3cef9-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="3cef9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="3cef9-133">In the search box, type **TurboRater**, select **TurboRater** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="3cef9-133">In the search box, type **TurboRater**, select **TurboRater** from result panel then click **Add** button to add the application.</span></span>

    ![TurboRater in the results list](./media/turborater-tutorial/tutorial_turborater_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3cef9-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3cef9-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3cef9-136">In this section, you configure and test Azure AD single sign-on with TurboRater based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3cef9-136">In this section, you configure and test Azure AD single sign-on with TurboRater based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3cef9-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TurboRater is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3cef9-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TurboRater is to a user in Azure AD.</span></span> <span data-ttu-id="3cef9-138">In other words, a link relationship between an Azure AD user and the related user in TurboRater needs to be established.</span><span class="sxs-lookup"><span data-stu-id="3cef9-138">In other words, a link relationship between an Azure AD user and the related user in TurboRater needs to be established.</span></span>

<span data-ttu-id="3cef9-139">In TurboRater, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="3cef9-139">In TurboRater, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3cef9-140">To configure and test Azure AD single sign-on with TurboRater, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="3cef9-140">To configure and test Azure AD single sign-on with TurboRater, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3cef9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="3cef9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="3cef9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3cef9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="3cef9-143">**[Create a TurboRater test user](#create-a-turborater-test-user)** - to have a counterpart of Britta Simon in TurboRater that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="3cef9-143">**[Create a TurboRater test user](#create-a-turborater-test-user)** - to have a counterpart of Britta Simon in TurboRater that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="3cef9-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3cef9-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="3cef9-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="3cef9-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3cef9-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3cef9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3cef9-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TurboRater application.</span><span class="sxs-lookup"><span data-stu-id="3cef9-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TurboRater application.</span></span>

<span data-ttu-id="3cef9-148">**To configure Azure AD single sign-on with TurboRater, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3cef9-148">**To configure Azure AD single sign-on with TurboRater, perform the following steps:**</span></span>

1. <span data-ttu-id="3cef9-149">In the Azure portal, on the **TurboRater** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3cef9-149">In the Azure portal, on the **TurboRater** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="3cef9-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3cef9-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/turborater-tutorial/tutorial_turborater_samlbase.png)

1. <span data-ttu-id="3cef9-153">On the **TurboRater Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3cef9-153">On the **TurboRater Domain and URLs** section, perform the following steps:</span></span>

    ![TurboRater Domain and URLs single sign-on information](./media/turborater-tutorial/tutorial_turborater_url.png)

    <span data-ttu-id="3cef9-155">a.</span><span class="sxs-lookup"><span data-stu-id="3cef9-155">a.</span></span> <span data-ttu-id="3cef9-156">In the **Identifier** textbox, type the value as: `https://www.itcdataservices.com`</span><span class="sxs-lookup"><span data-stu-id="3cef9-156">In the **Identifier** textbox, type the value as: `https://www.itcdataservices.com`</span></span>
 
    <span data-ttu-id="3cef9-157">b.</span><span class="sxs-lookup"><span data-stu-id="3cef9-157">b.</span></span> <span data-ttu-id="3cef9-158">In the **Reply URL** textbox, type the value as:</span><span class="sxs-lookup"><span data-stu-id="3cef9-158">In the **Reply URL** textbox, type the value as:</span></span>
    
    | <span data-ttu-id="3cef9-159">Environment</span><span class="sxs-lookup"><span data-stu-id="3cef9-159">Environment</span></span> | <span data-ttu-id="3cef9-160">URL</span><span class="sxs-lookup"><span data-stu-id="3cef9-160">URL</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="3cef9-161">Test</span><span class="sxs-lookup"><span data-stu-id="3cef9-161">Test</span></span>  | `https://ratingqa.itcdataservices.com/webservices/imp/saml/login` |
    | <span data-ttu-id="3cef9-162">Live</span><span class="sxs-lookup"><span data-stu-id="3cef9-162">Live</span></span>  | `https://www.itcratingservices.com/webservices/imp/saml/login` |

1. <span data-ttu-id="3cef9-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="3cef9-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/turborater-tutorial/tutorial_turborater_certificate.png) 

1. <span data-ttu-id="3cef9-165">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="3cef9-165">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/turborater-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="3cef9-167">To configure single sign-on on **TurboRater** side, you need to send the downloaded **Metadata XML** to [TurboRater support team](https://www.getitc.com/support).</span><span class="sxs-lookup"><span data-stu-id="3cef9-167">To configure single sign-on on **TurboRater** side, you need to send the downloaded **Metadata XML** to [TurboRater support team](https://www.getitc.com/support).</span></span> <span data-ttu-id="3cef9-168">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="3cef9-168">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3cef9-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="3cef9-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3cef9-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="3cef9-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3cef9-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3cef9-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3cef9-172">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3cef9-172">Create an Azure AD test user</span></span>

<span data-ttu-id="3cef9-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3cef9-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="3cef9-175">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3cef9-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3cef9-176">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="3cef9-176">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/turborater-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="3cef9-178">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="3cef9-178">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/turborater-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="3cef9-180">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="3cef9-180">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/turborater-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="3cef9-182">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3cef9-182">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/turborater-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3cef9-184">a.</span><span class="sxs-lookup"><span data-stu-id="3cef9-184">a.</span></span> <span data-ttu-id="3cef9-185">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3cef9-185">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3cef9-186">b.</span><span class="sxs-lookup"><span data-stu-id="3cef9-186">b.</span></span> <span data-ttu-id="3cef9-187">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3cef9-187">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="3cef9-188">c.</span><span class="sxs-lookup"><span data-stu-id="3cef9-188">c.</span></span> <span data-ttu-id="3cef9-189">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="3cef9-189">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="3cef9-190">d.</span><span class="sxs-lookup"><span data-stu-id="3cef9-190">d.</span></span> <span data-ttu-id="3cef9-191">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3cef9-191">Click **Create**.</span></span>
  
### <a name="create-a-turborater-test-user"></a><span data-ttu-id="3cef9-192">Create a TurboRater test user</span><span class="sxs-lookup"><span data-stu-id="3cef9-192">Create a TurboRater test user</span></span>

<span data-ttu-id="3cef9-193">To enable Azure AD users to log in to TurboRater, they must be provisioned into TurboRater.</span><span class="sxs-lookup"><span data-stu-id="3cef9-193">To enable Azure AD users to log in to TurboRater, they must be provisioned into TurboRater.</span></span>  
<span data-ttu-id="3cef9-194">In the case of TurboRater, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="3cef9-194">In the case of TurboRater, provisioning is a manual task.</span></span>
<span data-ttu-id="3cef9-195">To create a user, please work with [TurboRater support team](https://www.getitc.com/support).</span><span class="sxs-lookup"><span data-stu-id="3cef9-195">To create a user, please work with [TurboRater support team](https://www.getitc.com/support).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3cef9-196">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3cef9-196">Assign the Azure AD test user</span></span>

<span data-ttu-id="3cef9-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TurboRater.</span><span class="sxs-lookup"><span data-stu-id="3cef9-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TurboRater.</span></span>

![Assign the user role][200] 

<span data-ttu-id="3cef9-199">**To assign Britta Simon to TurboRater, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3cef9-199">**To assign Britta Simon to TurboRater, perform the following steps:**</span></span>

1. <span data-ttu-id="3cef9-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3cef9-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="3cef9-202">In the applications list, select **TurboRater**.</span><span class="sxs-lookup"><span data-stu-id="3cef9-202">In the applications list, select **TurboRater**.</span></span>

    ![The TurboRater link in the Applications list](./media/turborater-tutorial/tutorial_turborater_app.png)  

1. <span data-ttu-id="3cef9-204">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="3cef9-204">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="3cef9-206">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="3cef9-206">Click **Add** button.</span></span> <span data-ttu-id="3cef9-207">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3cef9-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="3cef9-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="3cef9-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="3cef9-210">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="3cef9-210">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="3cef9-211">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3cef9-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3cef9-212">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="3cef9-212">Test single sign-on</span></span>

<span data-ttu-id="3cef9-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3cef9-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3cef9-214">When you click the TurboRater tile in the Access Panel, you should get automatically signed-on to your TurboRater application.</span><span class="sxs-lookup"><span data-stu-id="3cef9-214">When you click the TurboRater tile in the Access Panel, you should get automatically signed-on to your TurboRater application.</span></span>
<span data-ttu-id="3cef9-215">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3cef9-215">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3cef9-216">Additional resources</span><span class="sxs-lookup"><span data-stu-id="3cef9-216">Additional resources</span></span>

* [<span data-ttu-id="3cef9-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3cef9-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="3cef9-218">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3cef9-218">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/turborater-tutorial/tutorial_general_01.png
[2]: ./media/turborater-tutorial/tutorial_general_02.png
[3]: ./media/turborater-tutorial/tutorial_general_03.png
[4]: ./media/turborater-tutorial/tutorial_general_04.png

[100]: ./media/turborater-tutorial/tutorial_general_100.png

[200]: ./media/turborater-tutorial/tutorial_general_200.png
[201]: ./media/turborater-tutorial/tutorial_general_201.png
[202]: ./media/turborater-tutorial/tutorial_general_202.png
[203]: ./media/turborater-tutorial/tutorial_general_203.png

