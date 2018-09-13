---
title: 'Tutorial: Azure Active Directory integration with Bynder | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Bynder.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 250dbdf2-faf5-48dd-be7c-d54502ef7528
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2017
ms.author: jeedes
ms.openlocfilehash: fadbd6a2b1e1a3197822552e4cd18ab765b696c8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868347"
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="edc47-103">Tutorial: Azure Active Directory integration with Bynder</span><span class="sxs-lookup"><span data-stu-id="edc47-103">Tutorial: Azure Active Directory integration with Bynder</span></span>

<span data-ttu-id="edc47-104">In this tutorial, you learn how to integrate Bynder with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="edc47-104">In this tutorial, you learn how to integrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="edc47-105">Integrating Bynder with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="edc47-105">Integrating Bynder with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="edc47-106">You can control in Azure AD who has access to Bynder.</span><span class="sxs-lookup"><span data-stu-id="edc47-106">You can control in Azure AD who has access to Bynder.</span></span>
- <span data-ttu-id="edc47-107">You can enable your users to automatically get signed-on to Bynder (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="edc47-107">You can enable your users to automatically get signed-on to Bynder (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="edc47-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="edc47-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="edc47-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="edc47-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edc47-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="edc47-110">Prerequisites</span></span>

<span data-ttu-id="edc47-111">To configure Azure AD integration with Bynder, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="edc47-111">To configure Azure AD integration with Bynder, you need the following items:</span></span>

- <span data-ttu-id="edc47-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="edc47-112">An Azure AD subscription</span></span>
- <span data-ttu-id="edc47-113">A Bynder single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="edc47-113">A Bynder single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="edc47-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="edc47-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="edc47-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="edc47-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="edc47-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="edc47-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="edc47-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="edc47-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="edc47-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="edc47-118">Scenario description</span></span>
<span data-ttu-id="edc47-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="edc47-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="edc47-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="edc47-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="edc47-121">Adding Bynder from the gallery</span><span class="sxs-lookup"><span data-stu-id="edc47-121">Adding Bynder from the gallery</span></span>
1. <span data-ttu-id="edc47-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="edc47-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bynder-from-the-gallery"></a><span data-ttu-id="edc47-123">Adding Bynder from the gallery</span><span class="sxs-lookup"><span data-stu-id="edc47-123">Adding Bynder from the gallery</span></span>
<span data-ttu-id="edc47-124">To configure the integration of Bynder into Azure AD, you need to add Bynder from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="edc47-124">To configure the integration of Bynder into Azure AD, you need to add Bynder from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="edc47-125">**To add Bynder from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="edc47-125">**To add Bynder from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="edc47-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="edc47-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="edc47-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="edc47-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="edc47-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="edc47-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="edc47-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="edc47-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="edc47-133">In the search box, type **Bynder**, select **Bynder** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="edc47-133">In the search box, type **Bynder**, select **Bynder** from result panel then click **Add** button to add the application.</span></span>

    ![Bynder in the results list](./media/bynder-tutorial/tutorial_bynder_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="edc47-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="edc47-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="edc47-136">In this section, you configure and test Azure AD single sign-on with Bynder based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="edc47-136">In this section, you configure and test Azure AD single sign-on with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="edc47-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Bynder is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="edc47-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Bynder is to a user in Azure AD.</span></span> <span data-ttu-id="edc47-138">In other words, a link relationship between an Azure AD user and the related user in Bynder needs to be established.</span><span class="sxs-lookup"><span data-stu-id="edc47-138">In other words, a link relationship between an Azure AD user and the related user in Bynder needs to be established.</span></span>

<span data-ttu-id="edc47-139">In Bynder, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="edc47-139">In Bynder, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="edc47-140">To configure and test Azure AD single sign-on with Bynder, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="edc47-140">To configure and test Azure AD single sign-on with Bynder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="edc47-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="edc47-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="edc47-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="edc47-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="edc47-143">**[Create a Bynder test user](#create-a-bynder-test-user)** - to have a counterpart of Britta Simon in Bynder that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="edc47-143">**[Create a Bynder test user](#create-a-bynder-test-user)** - to have a counterpart of Britta Simon in Bynder that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="edc47-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="edc47-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="edc47-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="edc47-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="edc47-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="edc47-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="edc47-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bynder application.</span><span class="sxs-lookup"><span data-stu-id="edc47-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bynder application.</span></span>

<span data-ttu-id="edc47-148">**To configure Azure AD single sign-on with Bynder, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="edc47-148">**To configure Azure AD single sign-on with Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="edc47-149">In the Azure portal, on the **Bynder** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="edc47-149">In the Azure portal, on the **Bynder** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="edc47-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="edc47-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/bynder-tutorial/tutorial_bynder_samlbase.png)

1. <span data-ttu-id="edc47-153">On the **Bynder Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="edc47-153">On the **Bynder Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Bynder Domain and URLs single sign-on information](./media/bynder-tutorial/tutorial_bynder_url.png)

    <span data-ttu-id="edc47-155">a.</span><span class="sxs-lookup"><span data-stu-id="edc47-155">a.</span></span> <span data-ttu-id="edc47-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com`</span><span class="sxs-lookup"><span data-stu-id="edc47-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com`</span></span>
    
    <span data-ttu-id="edc47-157">b.</span><span class="sxs-lookup"><span data-stu-id="edc47-157">b.</span></span> <span data-ttu-id="edc47-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="edc47-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>

1. <span data-ttu-id="edc47-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="edc47-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Bynder Domain and URLs single sign-on information](./media/bynder-tutorial/tutorial_bynder_url1.png)

    <span data-ttu-id="edc47-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/login/`</span><span class="sxs-lookup"><span data-stu-id="edc47-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/login/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="edc47-162">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="edc47-162">These values are not real.</span></span> <span data-ttu-id="edc47-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="edc47-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="edc47-164">Contact [Bynder Client support team](https://www.bynder.com/en/support/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="edc47-164">Contact [Bynder Client support team](https://www.bynder.com/en/support/) to get these values.</span></span> 

1. <span data-ttu-id="edc47-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="edc47-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/bynder-tutorial/tutorial_bynder_certificate.png) 

1. <span data-ttu-id="edc47-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="edc47-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/bynder-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="edc47-169">To configure single sign-on on **Bynder** side, you need to send the downloaded **Metadata XML** to [Bynder support team](https://www.bynder.com/en/support/).</span><span class="sxs-lookup"><span data-stu-id="edc47-169">To configure single sign-on on **Bynder** side, you need to send the downloaded **Metadata XML** to [Bynder support team](https://www.bynder.com/en/support/).</span></span> <span data-ttu-id="edc47-170">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="edc47-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="edc47-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="edc47-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="edc47-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="edc47-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="edc47-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="edc47-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="edc47-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="edc47-174">Create an Azure AD test user</span></span>

<span data-ttu-id="edc47-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="edc47-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="edc47-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="edc47-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="edc47-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="edc47-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/bynder-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="edc47-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="edc47-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/bynder-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="edc47-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="edc47-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/bynder-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="edc47-184">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="edc47-184">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/bynder-tutorial/create_aaduser_04.png)

    <span data-ttu-id="edc47-186">a.</span><span class="sxs-lookup"><span data-stu-id="edc47-186">a.</span></span> <span data-ttu-id="edc47-187">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="edc47-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="edc47-188">b.</span><span class="sxs-lookup"><span data-stu-id="edc47-188">b.</span></span> <span data-ttu-id="edc47-189">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="edc47-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="edc47-190">c.</span><span class="sxs-lookup"><span data-stu-id="edc47-190">c.</span></span> <span data-ttu-id="edc47-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="edc47-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="edc47-192">d.</span><span class="sxs-lookup"><span data-stu-id="edc47-192">d.</span></span> <span data-ttu-id="edc47-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="edc47-193">Click **Create**.</span></span>
 
### <a name="create-a-bynder-test-user"></a><span data-ttu-id="edc47-194">Create a Bynder test user</span><span class="sxs-lookup"><span data-stu-id="edc47-194">Create a Bynder test user</span></span>

<span data-ttu-id="edc47-195">The objective of this section is to create a user called Britta Simon in Bynder.</span><span class="sxs-lookup"><span data-stu-id="edc47-195">The objective of this section is to create a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="edc47-196">Bynder supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="edc47-196">Bynder supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="edc47-197">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="edc47-197">There is no action item for you in this section.</span></span> <span data-ttu-id="edc47-198">A new user will be created during an attempt to access Bynder if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="edc47-198">A new user will be created during an attempt to access Bynder if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="edc47-199">If you need to create a user manually, you need to contact the [Bynder support team](https://www.bynder.com/en/support/).</span><span class="sxs-lookup"><span data-stu-id="edc47-199">If you need to create a user manually, you need to contact the [Bynder support team](https://www.bynder.com/en/support/).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="edc47-200">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="edc47-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="edc47-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bynder.</span><span class="sxs-lookup"><span data-stu-id="edc47-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bynder.</span></span>

![Assign the user role][200] 

<span data-ttu-id="edc47-203">**To assign Britta Simon to Bynder, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="edc47-203">**To assign Britta Simon to Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="edc47-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="edc47-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="edc47-206">In the applications list, select **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="edc47-206">In the applications list, select **Bynder**.</span></span>

    ![The Bynder link in the Applications list](./media/bynder-tutorial/tutorial_bynder_app.png)  

1. <span data-ttu-id="edc47-208">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="edc47-208">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="edc47-210">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="edc47-210">Click **Add** button.</span></span> <span data-ttu-id="edc47-211">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="edc47-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="edc47-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="edc47-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="edc47-214">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="edc47-214">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="edc47-215">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="edc47-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="edc47-216">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="edc47-216">Test single sign-on</span></span>

<span data-ttu-id="edc47-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="edc47-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="edc47-218">When you click the Bynder tile in the Access Panel, you should get automatically signed-on to your Bynder application.</span><span class="sxs-lookup"><span data-stu-id="edc47-218">When you click the Bynder tile in the Access Panel, you should get automatically signed-on to your Bynder application.</span></span>
<span data-ttu-id="edc47-219">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="edc47-219">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="edc47-220">Additional resources</span><span class="sxs-lookup"><span data-stu-id="edc47-220">Additional resources</span></span>

* [<span data-ttu-id="edc47-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="edc47-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="edc47-222">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="edc47-222">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/bynder-tutorial/tutorial_general_01.png
[2]: ./media/bynder-tutorial/tutorial_general_02.png
[3]: ./media/bynder-tutorial/tutorial_general_03.png
[4]: ./media/bynder-tutorial/tutorial_general_04.png

[100]: ./media/bynder-tutorial/tutorial_general_100.png

[200]: ./media/bynder-tutorial/tutorial_general_200.png
[201]: ./media/bynder-tutorial/tutorial_general_201.png
[202]: ./media/bynder-tutorial/tutorial_general_202.png
[203]: ./media/bynder-tutorial/tutorial_general_203.png

