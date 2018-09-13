---
title: 'Tutorial: Azure Active Directory integration with Coupa | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Coupa.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2018
ms.author: jeedes
ms.openlocfilehash: 4bf40f76f5a8f788305b4dc9f91523f53fb59acf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866633"
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="b9764-103">Tutorial: Azure Active Directory integration with Coupa</span><span class="sxs-lookup"><span data-stu-id="b9764-103">Tutorial: Azure Active Directory integration with Coupa</span></span>

<span data-ttu-id="b9764-104">In this tutorial, you learn how to integrate Coupa with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b9764-104">In this tutorial, you learn how to integrate Coupa with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9764-105">Integrating Coupa with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="b9764-105">Integrating Coupa with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b9764-106">You can control in Azure AD who has access to Coupa.</span><span class="sxs-lookup"><span data-stu-id="b9764-106">You can control in Azure AD who has access to Coupa.</span></span>
- <span data-ttu-id="b9764-107">You can enable your users to automatically get signed-on to Coupa (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="b9764-107">You can enable your users to automatically get signed-on to Coupa (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b9764-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b9764-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b9764-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="b9764-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9764-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b9764-110">Prerequisites</span></span>

<span data-ttu-id="b9764-111">To configure Azure AD integration with Coupa, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="b9764-111">To configure Azure AD integration with Coupa, you need the following items:</span></span>

- <span data-ttu-id="b9764-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="b9764-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9764-113">A Coupa single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b9764-113">A Coupa single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9764-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="b9764-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9764-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="b9764-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9764-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="b9764-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b9764-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9764-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9764-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="b9764-118">Scenario description</span></span>
<span data-ttu-id="b9764-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="b9764-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9764-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="b9764-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9764-121">Adding Coupa from the gallery</span><span class="sxs-lookup"><span data-stu-id="b9764-121">Adding Coupa from the gallery</span></span>
1. <span data-ttu-id="b9764-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b9764-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-coupa-from-the-gallery"></a><span data-ttu-id="b9764-123">Adding Coupa from the gallery</span><span class="sxs-lookup"><span data-stu-id="b9764-123">Adding Coupa from the gallery</span></span>
<span data-ttu-id="b9764-124">To configure the integration of Coupa into Azure AD, you need to add Coupa from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="b9764-124">To configure the integration of Coupa into Azure AD, you need to add Coupa from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b9764-125">**To add Coupa from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b9764-125">**To add Coupa from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b9764-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="b9764-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="b9764-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="b9764-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b9764-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b9764-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

1. <span data-ttu-id="b9764-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="b9764-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="b9764-133">In the search box, type **Coupa**, select **Coupa** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="b9764-133">In the search box, type **Coupa**, select **Coupa** from result panel then click **Add** button to add the application.</span></span>

    ![Coupa in the results list](./media/coupa-tutorial/tutorial_coupa_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b9764-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b9764-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b9764-136">In this section, you configure and test Azure AD single sign-on with Coupa based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b9764-136">In this section, you configure and test Azure AD single sign-on with Coupa based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b9764-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Coupa is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9764-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Coupa is to a user in Azure AD.</span></span> <span data-ttu-id="b9764-138">In other words, a link relationship between an Azure AD user and the related user in Coupa needs to be established.</span><span class="sxs-lookup"><span data-stu-id="b9764-138">In other words, a link relationship between an Azure AD user and the related user in Coupa needs to be established.</span></span>

<span data-ttu-id="b9764-139">In Coupa, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="b9764-139">In Coupa, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b9764-140">To configure and test Azure AD single sign-on with Coupa, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b9764-140">To configure and test Azure AD single sign-on with Coupa, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b9764-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="b9764-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="b9764-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9764-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="b9764-143">**[Create a Coupa test user](#create-a-coupa-test-user)** - to have a counterpart of Britta Simon in Coupa that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="b9764-143">**[Create a Coupa test user](#create-a-coupa-test-user)** - to have a counterpart of Britta Simon in Coupa that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="b9764-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b9764-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="b9764-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="b9764-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b9764-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b9764-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b9764-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Coupa application.</span><span class="sxs-lookup"><span data-stu-id="b9764-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Coupa application.</span></span>

<span data-ttu-id="b9764-148">**To configure Azure AD single sign-on with Coupa, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b9764-148">**To configure Azure AD single sign-on with Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="b9764-149">In the Azure portal, on the **Coupa** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b9764-149">In the Azure portal, on the **Coupa** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="b9764-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b9764-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/coupa-tutorial/tutorial_coupa_samlbase.png)

1. <span data-ttu-id="b9764-153">On the **Coupa Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b9764-153">On the **Coupa Domain and URLs** section, perform the following steps:</span></span>

    ![Coupa Domain and URLs single sign-on information](./media/coupa-tutorial/tutorial_coupa_url.png)

    <span data-ttu-id="b9764-155">a.</span><span class="sxs-lookup"><span data-stu-id="b9764-155">a.</span></span> <span data-ttu-id="b9764-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.coupahost.com`</span><span class="sxs-lookup"><span data-stu-id="b9764-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.coupahost.com`</span></span>

    > [!NOTE]
    > <span data-ttu-id="b9764-157">The Sign-on URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="b9764-157">The Sign-on URL value is not real.</span></span> <span data-ttu-id="b9764-158">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="b9764-158">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="b9764-159">Contact [Coupa Client support team](https://success.coupa.com/Support/Contact_Us?) to get this value.</span><span class="sxs-lookup"><span data-stu-id="b9764-159">Contact [Coupa Client support team](https://success.coupa.com/Support/Contact_Us?) to get this value.</span></span>

    <span data-ttu-id="b9764-160">b.</span><span class="sxs-lookup"><span data-stu-id="b9764-160">b.</span></span> <span data-ttu-id="b9764-161">In the **Identifier** textbox, type the URL:</span><span class="sxs-lookup"><span data-stu-id="b9764-161">In the **Identifier** textbox, type the URL:</span></span>

    | <span data-ttu-id="b9764-162">Environment</span><span class="sxs-lookup"><span data-stu-id="b9764-162">Environment</span></span>  | <span data-ttu-id="b9764-163">URL</span><span class="sxs-lookup"><span data-stu-id="b9764-163">URL</span></span> |
    |:-------------|----|
    | <span data-ttu-id="b9764-164">Sandbox</span><span class="sxs-lookup"><span data-stu-id="b9764-164">Sandbox</span></span> | `devsso35.coupahost.com`|
    | <span data-ttu-id="b9764-165">Production</span><span class="sxs-lookup"><span data-stu-id="b9764-165">Production</span></span> | `prdsso40.coupahost.com`|
    | | |

    <span data-ttu-id="b9764-166">c.</span><span class="sxs-lookup"><span data-stu-id="b9764-166">c.</span></span> <span data-ttu-id="b9764-167">In the **Reply URL** textbox, type the URL:</span><span class="sxs-lookup"><span data-stu-id="b9764-167">In the **Reply URL** textbox, type the URL:</span></span>

    | <span data-ttu-id="b9764-168">Environment</span><span class="sxs-lookup"><span data-stu-id="b9764-168">Environment</span></span> | <span data-ttu-id="b9764-169">URL</span><span class="sxs-lookup"><span data-stu-id="b9764-169">URL</span></span> |
    |------------- |----|
    | <span data-ttu-id="b9764-170">Sandbox</span><span class="sxs-lookup"><span data-stu-id="b9764-170">Sandbox</span></span> | `https://devsso35.coupahost.com/sp/ACS.saml2`|
    | <span data-ttu-id="b9764-171">Production</span><span class="sxs-lookup"><span data-stu-id="b9764-171">Production</span></span> | `https://prdsso40.coupahost.com/sp/ACS.saml2`|
    | | |

1. <span data-ttu-id="b9764-172">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="b9764-172">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/coupa-tutorial/tutorial_coupa_certificate.png) 

1. <span data-ttu-id="b9764-174">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="b9764-174">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/coupa-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="b9764-176">Sign on to your Coupa company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="b9764-176">Sign on to your Coupa company site as an administrator.</span></span>

1. <span data-ttu-id="b9764-177">Go to **Setup \> Security Control**.</span><span class="sxs-lookup"><span data-stu-id="b9764-177">Go to **Setup \> Security Control**.</span></span>

   <span data-ttu-id="b9764-178">![Security Controls](./media/coupa-tutorial/ic791900.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="b9764-178">![Security Controls](./media/coupa-tutorial/ic791900.png "Security Controls")</span></span>

1. <span data-ttu-id="b9764-179">In the **Log in using Coupa credentials** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b9764-179">In the **Log in using Coupa credentials** section, perform the following steps:</span></span>

    <span data-ttu-id="b9764-180">![Coupa SP metadata](./media/coupa-tutorial/ic791901.png "Coupa SP metadata")</span><span class="sxs-lookup"><span data-stu-id="b9764-180">![Coupa SP metadata](./media/coupa-tutorial/ic791901.png "Coupa SP metadata")</span></span>

    <span data-ttu-id="b9764-181">a.</span><span class="sxs-lookup"><span data-stu-id="b9764-181">a.</span></span> <span data-ttu-id="b9764-182">Select **Log in using SAML**.</span><span class="sxs-lookup"><span data-stu-id="b9764-182">Select **Log in using SAML**.</span></span>

    <span data-ttu-id="b9764-183">b.</span><span class="sxs-lookup"><span data-stu-id="b9764-183">b.</span></span> <span data-ttu-id="b9764-184">Click **Browse** to upload the metadata downloaded from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b9764-184">Click **Browse** to upload the metadata downloaded from the Azure portal.</span></span>

    <span data-ttu-id="b9764-185">c.</span><span class="sxs-lookup"><span data-stu-id="b9764-185">c.</span></span> <span data-ttu-id="b9764-186">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b9764-186">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b9764-187">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b9764-187">Create an Azure AD test user</span></span>

<span data-ttu-id="b9764-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9764-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="b9764-190">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b9764-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b9764-191">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="b9764-191">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/coupa-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="b9764-193">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="b9764-193">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/coupa-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="b9764-195">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="b9764-195">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/coupa-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="b9764-197">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b9764-197">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/coupa-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b9764-199">a.</span><span class="sxs-lookup"><span data-stu-id="b9764-199">a.</span></span> <span data-ttu-id="b9764-200">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b9764-200">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9764-201">b.</span><span class="sxs-lookup"><span data-stu-id="b9764-201">b.</span></span> <span data-ttu-id="b9764-202">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9764-202">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b9764-203">c.</span><span class="sxs-lookup"><span data-stu-id="b9764-203">c.</span></span> <span data-ttu-id="b9764-204">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="b9764-204">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b9764-205">d.</span><span class="sxs-lookup"><span data-stu-id="b9764-205">d.</span></span> <span data-ttu-id="b9764-206">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b9764-206">Click **Create**.</span></span>

### <a name="create-a-coupa-test-user"></a><span data-ttu-id="b9764-207">Create a Coupa test user</span><span class="sxs-lookup"><span data-stu-id="b9764-207">Create a Coupa test user</span></span>

<span data-ttu-id="b9764-208">In order to enable Azure AD users to log into Coupa, they must be provisioned into Coupa.</span><span class="sxs-lookup"><span data-stu-id="b9764-208">In order to enable Azure AD users to log into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="b9764-209">In the case of Coupa, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="b9764-209">In the case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="b9764-210">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b9764-210">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="b9764-211">Log in to your **Coupa** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="b9764-211">Log in to your **Coupa** company site as administrator.</span></span>

1. <span data-ttu-id="b9764-212">In the menu on the top, click **Setup**, and then click **Users**.</span><span class="sxs-lookup"><span data-stu-id="b9764-212">In the menu on the top, click **Setup**, and then click **Users**.</span></span>

   <span data-ttu-id="b9764-213">![Users](./media/coupa-tutorial/ic791908.png "Users")</span><span class="sxs-lookup"><span data-stu-id="b9764-213">![Users](./media/coupa-tutorial/ic791908.png "Users")</span></span>

1. <span data-ttu-id="b9764-214">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b9764-214">Click **Create**.</span></span>

   <span data-ttu-id="b9764-215">![Create Users](./media/coupa-tutorial/ic791909.png "Create Users")</span><span class="sxs-lookup"><span data-stu-id="b9764-215">![Create Users](./media/coupa-tutorial/ic791909.png "Create Users")</span></span>

1. <span data-ttu-id="b9764-216">In the **User Create** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b9764-216">In the **User Create** section, perform the following steps:</span></span>

   <span data-ttu-id="b9764-217">![User Details](./media/coupa-tutorial/ic791910.png "User Details")</span><span class="sxs-lookup"><span data-stu-id="b9764-217">![User Details](./media/coupa-tutorial/ic791910.png "User Details")</span></span>

   <span data-ttu-id="b9764-218">a.</span><span class="sxs-lookup"><span data-stu-id="b9764-218">a.</span></span> <span data-ttu-id="b9764-219">Type the **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="b9764-219">Type the **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>

   <span data-ttu-id="b9764-220">b.</span><span class="sxs-lookup"><span data-stu-id="b9764-220">b.</span></span> <span data-ttu-id="b9764-221">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b9764-221">Click **Create**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="b9764-222">The Azure Active Directory account holder will get an email with a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="b9764-222">The Azure Active Directory account holder will get an email with a link to confirm the account before it becomes active.</span></span>
   >

>[!NOTE]
><span data-ttu-id="b9764-223">You can use any other Coupa user account creation tools or APIs provided by Coupa to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="b9764-223">You can use any other Coupa user account creation tools or APIs provided by Coupa to provision AAD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b9764-224">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b9764-224">Assign the Azure AD test user</span></span>

<span data-ttu-id="b9764-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Coupa.</span><span class="sxs-lookup"><span data-stu-id="b9764-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Coupa.</span></span>

![Assign the user role][200]

<span data-ttu-id="b9764-227">**To assign Britta Simon to Coupa, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b9764-227">**To assign Britta Simon to Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="b9764-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b9764-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

1. <span data-ttu-id="b9764-230">In the applications list, select **Coupa**.</span><span class="sxs-lookup"><span data-stu-id="b9764-230">In the applications list, select **Coupa**.</span></span>

    ![The Coupa link in the Applications list](./media/coupa-tutorial/tutorial_coupa_app.png)  

1. <span data-ttu-id="b9764-232">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="b9764-232">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="b9764-234">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="b9764-234">Click **Add** button.</span></span> <span data-ttu-id="b9764-235">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b9764-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="b9764-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="b9764-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="b9764-238">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="b9764-238">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="b9764-239">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b9764-239">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="b9764-240">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="b9764-240">Test single sign-on</span></span>

<span data-ttu-id="b9764-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b9764-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b9764-242">When you click the Coupa tile in the Access Panel, you should get automatically signed-on to your Coupa application.</span><span class="sxs-lookup"><span data-stu-id="b9764-242">When you click the Coupa tile in the Access Panel, you should get automatically signed-on to your Coupa application.</span></span>
<span data-ttu-id="b9764-243">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b9764-243">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b9764-244">Additional resources</span><span class="sxs-lookup"><span data-stu-id="b9764-244">Additional resources</span></span>

* [<span data-ttu-id="b9764-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9764-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="b9764-246">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b9764-246">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/coupa-tutorial/tutorial_general_01.png
[2]: ./media/coupa-tutorial/tutorial_general_02.png
[3]: ./media/coupa-tutorial/tutorial_general_03.png
[4]: ./media/coupa-tutorial/tutorial_general_04.png

[100]: ./media/coupa-tutorial/tutorial_general_100.png

[200]: ./media/coupa-tutorial/tutorial_general_200.png
[201]: ./media/coupa-tutorial/tutorial_general_201.png
[202]: ./media/coupa-tutorial/tutorial_general_202.png
[203]: ./media/coupa-tutorial/tutorial_general_203.png
