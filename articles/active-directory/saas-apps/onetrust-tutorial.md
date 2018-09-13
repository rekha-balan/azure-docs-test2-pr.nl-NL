---
title: 'Tutorial: Azure Active Directory integration with OneTrust Privacy Management Software | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and OneTrust Privacy Management Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71c2b6d0-3d28-4130-a2c8-1e72ab3d5814
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2017
ms.author: jeedes
ms.openlocfilehash: f8e06a4578d2f11331b87fdfb493e2bba4edb8cf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857626"
---
# <a name="tutorial-azure-active-directory-integration-with-onetrust-privacy-management-software"></a><span data-ttu-id="61139-103">Tutorial: Azure Active Directory integration with OneTrust Privacy Management Software</span><span class="sxs-lookup"><span data-stu-id="61139-103">Tutorial: Azure Active Directory integration with OneTrust Privacy Management Software</span></span>

<span data-ttu-id="61139-104">In this tutorial, you learn how to integrate OneTrust Privacy Management Software with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="61139-104">In this tutorial, you learn how to integrate OneTrust Privacy Management Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="61139-105">Integrating OneTrust Privacy Management Software with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="61139-105">Integrating OneTrust Privacy Management Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="61139-106">You can control in Azure AD who has access to OneTrust Privacy Management Software.</span><span class="sxs-lookup"><span data-stu-id="61139-106">You can control in Azure AD who has access to OneTrust Privacy Management Software.</span></span>
- <span data-ttu-id="61139-107">You can enable your users to automatically get signed-on to OneTrust Privacy Management Software (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="61139-107">You can enable your users to automatically get signed-on to OneTrust Privacy Management Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="61139-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="61139-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="61139-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="61139-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61139-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="61139-110">Prerequisites</span></span>

<span data-ttu-id="61139-111">To configure Azure AD integration with OneTrust Privacy Management Software, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="61139-111">To configure Azure AD integration with OneTrust Privacy Management Software, you need the following items:</span></span>

- <span data-ttu-id="61139-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="61139-112">An Azure AD subscription</span></span>
- <span data-ttu-id="61139-113">A OneTrust Privacy Management Software single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="61139-113">A OneTrust Privacy Management Software single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="61139-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="61139-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="61139-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="61139-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="61139-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="61139-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="61139-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="61139-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="61139-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="61139-118">Scenario description</span></span>
<span data-ttu-id="61139-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="61139-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="61139-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="61139-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="61139-121">Adding OneTrust Privacy Management Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="61139-121">Adding OneTrust Privacy Management Software from the gallery</span></span>
1. <span data-ttu-id="61139-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="61139-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-onetrust-privacy-management-software-from-the-gallery"></a><span data-ttu-id="61139-123">Adding OneTrust Privacy Management Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="61139-123">Adding OneTrust Privacy Management Software from the gallery</span></span>
<span data-ttu-id="61139-124">To configure the integration of OneTrust Privacy Management Software into Azure AD, you need to add OneTrust Privacy Management Software from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="61139-124">To configure the integration of OneTrust Privacy Management Software into Azure AD, you need to add OneTrust Privacy Management Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="61139-125">**To add OneTrust Privacy Management Software from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61139-125">**To add OneTrust Privacy Management Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="61139-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="61139-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="61139-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="61139-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="61139-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="61139-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="61139-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="61139-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="61139-133">In the search box, type **OneTrust Privacy Management Software**, select **OneTrust Privacy Management Software** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="61139-133">In the search box, type **OneTrust Privacy Management Software**, select **OneTrust Privacy Management Software** from result panel then click **Add** button to add the application.</span></span>

    ![OneTrust Privacy Management Software in the results list](./media/onetrust-tutorial/tutorial_onetrust_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="61139-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="61139-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="61139-136">In this section, you configure and test Azure AD single sign-on with OneTrust Privacy Management Software based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="61139-136">In this section, you configure and test Azure AD single sign-on with OneTrust Privacy Management Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="61139-137">For single sign-on to work, Azure AD needs to know what the counterpart user in OneTrust Privacy Management Software is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61139-137">For single sign-on to work, Azure AD needs to know what the counterpart user in OneTrust Privacy Management Software is to a user in Azure AD.</span></span> <span data-ttu-id="61139-138">In other words, a link relationship between an Azure AD user and the related user in OneTrust Privacy Management Software needs to be established.</span><span class="sxs-lookup"><span data-stu-id="61139-138">In other words, a link relationship between an Azure AD user and the related user in OneTrust Privacy Management Software needs to be established.</span></span>

<span data-ttu-id="61139-139">In OneTrust Privacy Management Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="61139-139">In OneTrust Privacy Management Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="61139-140">To configure and test Azure AD single sign-on with OneTrust Privacy Management Software, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="61139-140">To configure and test Azure AD single sign-on with OneTrust Privacy Management Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="61139-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="61139-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="61139-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="61139-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="61139-143">**[Create a OneTrust Privacy Management Software test user](#create-a-onetrust-privacy-management-software-test-user)** - to have a counterpart of Britta Simon in OneTrust Privacy Management Software that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="61139-143">**[Create a OneTrust Privacy Management Software test user](#create-a-onetrust-privacy-management-software-test-user)** - to have a counterpart of Britta Simon in OneTrust Privacy Management Software that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="61139-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="61139-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="61139-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="61139-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="61139-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="61139-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="61139-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OneTrust Privacy Management Software application.</span><span class="sxs-lookup"><span data-stu-id="61139-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OneTrust Privacy Management Software application.</span></span>

<span data-ttu-id="61139-148">**To configure Azure AD single sign-on with OneTrust Privacy Management Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61139-148">**To configure Azure AD single sign-on with OneTrust Privacy Management Software, perform the following steps:**</span></span>

1. <span data-ttu-id="61139-149">In the Azure portal, on the **OneTrust Privacy Management Software** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="61139-149">In the Azure portal, on the **OneTrust Privacy Management Software** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="61139-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="61139-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/onetrust-tutorial/tutorial_onetrust_samlbase.png)

1. <span data-ttu-id="61139-153">On the **OneTrust Privacy Management Software Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="61139-153">On the **OneTrust Privacy Management Software Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![OneTrust Privacy Management Software Domain and URLs single sign-on information](./media/onetrust-tutorial/tutorial_onetrust_url.png)

    <span data-ttu-id="61139-155">a.</span><span class="sxs-lookup"><span data-stu-id="61139-155">a.</span></span> <span data-ttu-id="61139-156">In the **Identifier** textbox, type a URL: `https://www.onetrust.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="61139-156">In the **Identifier** textbox, type a URL: `https://www.onetrust.com/saml2`</span></span>

    <span data-ttu-id="61139-157">b.</span><span class="sxs-lookup"><span data-stu-id="61139-157">b.</span></span> <span data-ttu-id="61139-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.onetrust.com/auth/consumerservice`</span><span class="sxs-lookup"><span data-stu-id="61139-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.onetrust.com/auth/consumerservice`</span></span>

1. <span data-ttu-id="61139-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="61139-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![OneTrust Privacy Management Software Domain and URLs single sign-on information](./media/onetrust-tutorial/tutorial_onetrust_url1.png)

    <span data-ttu-id="61139-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.onetrust.com/auth/login`</span><span class="sxs-lookup"><span data-stu-id="61139-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.onetrust.com/auth/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="61139-162">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="61139-162">These values are not real.</span></span> <span data-ttu-id="61139-163">Update these values with the actual Reply URL and Sign on URL.</span><span class="sxs-lookup"><span data-stu-id="61139-163">Update these values with the actual Reply URL and Sign on URL.</span></span> <span data-ttu-id="61139-164">Contact [OneTrust Privacy Management Software Client support team](mailto:support@onetrust.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="61139-164">Contact [OneTrust Privacy Management Software Client support team](mailto:support@onetrust.com) to get these values.</span></span> 

1. <span data-ttu-id="61139-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="61139-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/onetrust-tutorial/tutorial_onetrust_certificate.png) 

1. <span data-ttu-id="61139-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="61139-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/onetrust-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="61139-169">To configure single sign-on on **OneTrust Privacy Management Software** side, you need to send the downloaded **Metadata XML** to [OneTrust Privacy Management Software support team](mailto:support@onetrust.com).</span><span class="sxs-lookup"><span data-stu-id="61139-169">To configure single sign-on on **OneTrust Privacy Management Software** side, you need to send the downloaded **Metadata XML** to [OneTrust Privacy Management Software support team](mailto:support@onetrust.com).</span></span> <span data-ttu-id="61139-170">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="61139-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="61139-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="61139-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="61139-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="61139-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="61139-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="61139-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="61139-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="61139-174">Create an Azure AD test user</span></span>

<span data-ttu-id="61139-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="61139-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="61139-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61139-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="61139-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="61139-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/onetrust-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="61139-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="61139-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/onetrust-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="61139-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="61139-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/onetrust-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="61139-184">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="61139-184">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/onetrust-tutorial/create_aaduser_04.png)

    <span data-ttu-id="61139-186">a.</span><span class="sxs-lookup"><span data-stu-id="61139-186">a.</span></span> <span data-ttu-id="61139-187">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="61139-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="61139-188">b.</span><span class="sxs-lookup"><span data-stu-id="61139-188">b.</span></span> <span data-ttu-id="61139-189">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="61139-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="61139-190">c.</span><span class="sxs-lookup"><span data-stu-id="61139-190">c.</span></span> <span data-ttu-id="61139-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="61139-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="61139-192">d.</span><span class="sxs-lookup"><span data-stu-id="61139-192">d.</span></span> <span data-ttu-id="61139-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="61139-193">Click **Create**.</span></span>
 
### <a name="create-a-onetrust-privacy-management-software-test-user"></a><span data-ttu-id="61139-194">Create a OneTrust Privacy Management Software test user</span><span class="sxs-lookup"><span data-stu-id="61139-194">Create a OneTrust Privacy Management Software test user</span></span>

<span data-ttu-id="61139-195">The objective of this section is to create a user called Britta Simon in OneTrust Privacy Management Software.</span><span class="sxs-lookup"><span data-stu-id="61139-195">The objective of this section is to create a user called Britta Simon in OneTrust Privacy Management Software.</span></span> <span data-ttu-id="61139-196">OneTrust Privacy Management Software supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="61139-196">OneTrust Privacy Management Software supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="61139-197">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="61139-197">There is no action item for you in this section.</span></span> <span data-ttu-id="61139-198">A new user is created during an attempt to access OneTrust Privacy Management Software if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="61139-198">A new user is created during an attempt to access OneTrust Privacy Management Software if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="61139-199">If you need to create a user manually, Contact [OneTrust Privacy Management Software support team](mailto:support@onetrust.com).</span><span class="sxs-lookup"><span data-stu-id="61139-199">If you need to create a user manually, Contact [OneTrust Privacy Management Software support team](mailto:support@onetrust.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="61139-200">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="61139-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="61139-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OneTrust Privacy Management Software.</span><span class="sxs-lookup"><span data-stu-id="61139-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OneTrust Privacy Management Software.</span></span>

![Assign the user role][200] 

<span data-ttu-id="61139-203">**To assign Britta Simon to OneTrust Privacy Management Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61139-203">**To assign Britta Simon to OneTrust Privacy Management Software, perform the following steps:**</span></span>

1. <span data-ttu-id="61139-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="61139-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="61139-206">In the applications list, select **OneTrust Privacy Management Software**.</span><span class="sxs-lookup"><span data-stu-id="61139-206">In the applications list, select **OneTrust Privacy Management Software**.</span></span>

    ![The OneTrust Privacy Management Software link in the Applications list](./media/onetrust-tutorial/tutorial_onetrust_app.png)  

1. <span data-ttu-id="61139-208">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="61139-208">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="61139-210">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="61139-210">Click **Add** button.</span></span> <span data-ttu-id="61139-211">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="61139-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="61139-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="61139-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="61139-214">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="61139-214">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="61139-215">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="61139-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="61139-216">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="61139-216">Test single sign-on</span></span>

<span data-ttu-id="61139-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="61139-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="61139-218">When you click the OneTrust Privacy Management Software tile in the Access Panel, you should get automatically signed-on to your OneTrust Privacy Management Software application.</span><span class="sxs-lookup"><span data-stu-id="61139-218">When you click the OneTrust Privacy Management Software tile in the Access Panel, you should get automatically signed-on to your OneTrust Privacy Management Software application.</span></span>
<span data-ttu-id="61139-219">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="61139-219">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="61139-220">Additional resources</span><span class="sxs-lookup"><span data-stu-id="61139-220">Additional resources</span></span>

* [<span data-ttu-id="61139-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="61139-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="61139-222">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="61139-222">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/onetrust-tutorial/tutorial_general_01.png
[2]: ./media/onetrust-tutorial/tutorial_general_02.png
[3]: ./media/onetrust-tutorial/tutorial_general_03.png
[4]: ./media/onetrust-tutorial/tutorial_general_04.png

[100]: ./media/onetrust-tutorial/tutorial_general_100.png

[200]: ./media/onetrust-tutorial/tutorial_general_200.png
[201]: ./media/onetrust-tutorial/tutorial_general_201.png
[202]: ./media/onetrust-tutorial/tutorial_general_202.png
[203]: ./media/onetrust-tutorial/tutorial_general_203.png

