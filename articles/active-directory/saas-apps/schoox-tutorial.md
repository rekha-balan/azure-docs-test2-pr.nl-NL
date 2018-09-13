---
title: 'Tutorial: Azure Active Directory integration with Schoox | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Schoox.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: f8b4cdcc-cbf6-4229-9427-05632e33f942
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/09/2017
ms.author: jeedes
ms.openlocfilehash: 3f26809d934708ecad2e3dda69a8cfc25e02d58a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867399"
---
# <a name="tutorial-azure-active-directory-integration-with-schoox"></a><span data-ttu-id="f0c1e-103">Tutorial: Azure Active Directory integration with Schoox</span><span class="sxs-lookup"><span data-stu-id="f0c1e-103">Tutorial: Azure Active Directory integration with Schoox</span></span>

<span data-ttu-id="f0c1e-104">In this tutorial, you learn how to integrate Schoox with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f0c1e-104">In this tutorial, you learn how to integrate Schoox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f0c1e-105">Integrating Schoox with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f0c1e-105">Integrating Schoox with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f0c1e-106">You can control in Azure AD who has access to Schoox.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-106">You can control in Azure AD who has access to Schoox.</span></span>
- <span data-ttu-id="f0c1e-107">You can enable your users to automatically get signed-on to Schoox (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-107">You can enable your users to automatically get signed-on to Schoox (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f0c1e-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f0c1e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="f0c1e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0c1e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f0c1e-110">Prerequisites</span></span>

<span data-ttu-id="f0c1e-111">To configure Azure AD integration with Schoox, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f0c1e-111">To configure Azure AD integration with Schoox, you need the following items:</span></span>

- <span data-ttu-id="f0c1e-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f0c1e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f0c1e-113">A Schoox single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f0c1e-113">A Schoox single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f0c1e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f0c1e-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f0c1e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f0c1e-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f0c1e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f0c1e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f0c1e-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f0c1e-118">Scenario description</span></span>
<span data-ttu-id="f0c1e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f0c1e-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f0c1e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f0c1e-121">Adding Schoox from the gallery</span><span class="sxs-lookup"><span data-stu-id="f0c1e-121">Adding Schoox from the gallery</span></span>
2. <span data-ttu-id="f0c1e-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f0c1e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-schoox-from-the-gallery"></a><span data-ttu-id="f0c1e-123">Adding Schoox from the gallery</span><span class="sxs-lookup"><span data-stu-id="f0c1e-123">Adding Schoox from the gallery</span></span>
<span data-ttu-id="f0c1e-124">To configure the integration of Schoox into Azure AD, you need to add Schoox from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-124">To configure the integration of Schoox into Azure AD, you need to add Schoox from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f0c1e-125">**To add Schoox from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f0c1e-125">**To add Schoox from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f0c1e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="f0c1e-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f0c1e-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="f0c1e-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="f0c1e-133">In the search box, type **Schoox**, select **Schoox** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-133">In the search box, type **Schoox**, select **Schoox** from result panel then click **Add** button to add the application.</span></span>

    ![Schoox in the results list](./media/schoox-tutorial/tutorial_schoox_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f0c1e-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f0c1e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f0c1e-136">In this section, you configure and test Azure AD single sign-on with Schoox based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="f0c1e-136">In this section, you configure and test Azure AD single sign-on with Schoox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f0c1e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Schoox is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Schoox is to a user in Azure AD.</span></span> <span data-ttu-id="f0c1e-138">In other words, a link relationship between an Azure AD user and the related user in Schoox needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-138">In other words, a link relationship between an Azure AD user and the related user in Schoox needs to be established.</span></span>

<span data-ttu-id="f0c1e-139">In Schoox, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-139">In Schoox, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f0c1e-140">To configure and test Azure AD single sign-on with Schoox, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f0c1e-140">To configure and test Azure AD single sign-on with Schoox, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f0c1e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f0c1e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f0c1e-143">**[Create a Schoox test user](#create-a-schoox-test-user)** - to have a counterpart of Britta Simon in Schoox that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-143">**[Create a Schoox test user](#create-a-schoox-test-user)** - to have a counterpart of Britta Simon in Schoox that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f0c1e-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f0c1e-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f0c1e-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f0c1e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f0c1e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Schoox application.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Schoox application.</span></span>

<span data-ttu-id="f0c1e-148">**To configure Azure AD single sign-on with Schoox, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f0c1e-148">**To configure Azure AD single sign-on with Schoox, perform the following steps:**</span></span>

1. <span data-ttu-id="f0c1e-149">In the Azure portal, on the **Schoox** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-149">In the Azure portal, on the **Schoox** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="f0c1e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/schoox-tutorial/tutorial_schoox_samlbase.png)

3. <span data-ttu-id="f0c1e-153">On the **Schoox Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="f0c1e-153">On the **Schoox Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Schoox Domain and URLs single sign-on information](./media/schoox-tutorial/tutorial_schoox_url.png)

    <span data-ttu-id="f0c1e-155">In the **Identifier** textbox, type a URL : `https://saml.schoox.com/saml/adfsmetadata`</span><span class="sxs-lookup"><span data-stu-id="f0c1e-155">In the **Identifier** textbox, type a URL : `https://saml.schoox.com/saml/adfsmetadata`</span></span>

4. <span data-ttu-id="f0c1e-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="f0c1e-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Schoox Domain and URLs single sign-on information](./media/schoox-tutorial/tutorial_schoox_url1.png)

    <span data-ttu-id="f0c1e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://saml.schoox.com/saml/login?idpUrl=<entityID>`</span><span class="sxs-lookup"><span data-stu-id="f0c1e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://saml.schoox.com/saml/login?idpUrl=<entityID>`</span></span>
    
    > [!Note]
    > <span data-ttu-id="f0c1e-159">`<entityID>` is the SAML Entity ID copied from the Quick Reference section, described later in tutorial.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-159">`<entityID>` is the SAML Entity ID copied from the Quick Reference section, described later in tutorial.</span></span> 

5. <span data-ttu-id="f0c1e-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/schoox-tutorial/tutorial_schoox_certificate.png) 

6. <span data-ttu-id="f0c1e-162">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-162">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/schoox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f0c1e-164">On the **Schoox Configuration** section, click **Configure Schoox** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-164">On the **Schoox Configuration** section, click **Configure Schoox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f0c1e-165">Copy the **SAML Entity ID** from the **Quick Reference section** and use it to complete **Sign-on URL** in **Schoox Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-165">Copy the **SAML Entity ID** from the **Quick Reference section** and use it to complete **Sign-on URL** in **Schoox Domain and URLs** section.</span></span> 

    ![Schoox Configuration](./media/schoox-tutorial/config.png)

8. <span data-ttu-id="f0c1e-167">To configure single sign-on on **Schoox** side, you need to send the downloaded **Metadata XML** to [Schoox support team](https://www.schoox.com/help/).</span><span class="sxs-lookup"><span data-stu-id="f0c1e-167">To configure single sign-on on **Schoox** side, you need to send the downloaded **Metadata XML** to [Schoox support team](https://www.schoox.com/help/).</span></span> <span data-ttu-id="f0c1e-168">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-168">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f0c1e-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="f0c1e-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f0c1e-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f0c1e-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f0c1e-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f0c1e-172">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f0c1e-172">Create an Azure AD test user</span></span>

<span data-ttu-id="f0c1e-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="f0c1e-175">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f0c1e-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f0c1e-176">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-176">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/schoox-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f0c1e-178">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-178">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/schoox-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f0c1e-180">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-180">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/schoox-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f0c1e-182">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f0c1e-182">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/schoox-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f0c1e-184">a.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-184">a.</span></span> <span data-ttu-id="f0c1e-185">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-185">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f0c1e-186">b.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-186">b.</span></span> <span data-ttu-id="f0c1e-187">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-187">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f0c1e-188">c.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-188">c.</span></span> <span data-ttu-id="f0c1e-189">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-189">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f0c1e-190">d.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-190">d.</span></span> <span data-ttu-id="f0c1e-191">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-191">Click **Create**.</span></span>
 
### <a name="create-a-schoox-test-user"></a><span data-ttu-id="f0c1e-192">Create a Schoox test user</span><span class="sxs-lookup"><span data-stu-id="f0c1e-192">Create a Schoox test user</span></span>

<span data-ttu-id="f0c1e-193">In this section, you create a user called Britta Simon in Schoox.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-193">In this section, you create a user called Britta Simon in Schoox.</span></span> <span data-ttu-id="f0c1e-194">Work with [Schoox support team](https://www.schoox.com/help/) to add the users in the Schoox platform.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-194">Work with [Schoox support team](https://www.schoox.com/help/) to add the users in the Schoox platform.</span></span> <span data-ttu-id="f0c1e-195">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-195">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f0c1e-196">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f0c1e-196">Assign the Azure AD test user</span></span>

<span data-ttu-id="f0c1e-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Schoox.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Schoox.</span></span>

![Assign the user role][200] 

<span data-ttu-id="f0c1e-199">**To assign Britta Simon to Schoox, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f0c1e-199">**To assign Britta Simon to Schoox, perform the following steps:**</span></span>

1. <span data-ttu-id="f0c1e-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="f0c1e-202">In the applications list, select **Schoox**.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-202">In the applications list, select **Schoox**.</span></span>

    ![The Schoox link in the Applications list](./media/schoox-tutorial/tutorial_schoox_app.png)  

3. <span data-ttu-id="f0c1e-204">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-204">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="f0c1e-206">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-206">Click **Add** button.</span></span> <span data-ttu-id="f0c1e-207">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="f0c1e-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f0c1e-210">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f0c1e-211">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f0c1e-212">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="f0c1e-212">Test single sign-on</span></span>

<span data-ttu-id="f0c1e-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f0c1e-214">When you click the Schoox tile in the Access Panel, you should get automatically signed-on to your Schoox application.</span><span class="sxs-lookup"><span data-stu-id="f0c1e-214">When you click the Schoox tile in the Access Panel, you should get automatically signed-on to your Schoox application.</span></span>
<span data-ttu-id="f0c1e-215">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f0c1e-215">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f0c1e-216">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f0c1e-216">Additional resources</span></span>

* [<span data-ttu-id="f0c1e-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0c1e-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="f0c1e-218">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f0c1e-218">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/schoox-tutorial/tutorial_general_01.png
[2]: ./media/schoox-tutorial/tutorial_general_02.png
[3]: ./media/schoox-tutorial/tutorial_general_03.png
[4]: ./media/schoox-tutorial/tutorial_general_04.png

[100]: ./media/schoox-tutorial/tutorial_general_100.png

[200]: ./media/schoox-tutorial/tutorial_general_200.png
[201]: ./media/schoox-tutorial/tutorial_general_201.png
[202]: ./media/schoox-tutorial/tutorial_general_202.png
[203]: ./media/schoox-tutorial/tutorial_general_203.png

