---
title: 'Tutorial: Azure Active Directory integration with AwardSpring | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and AwardSpring.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2f115be6-4fbe-42aa-9319-7462e7a75736
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2018
ms.author: jeedes
ms.openlocfilehash: f75c14989b46721e7043c06086cac02222f452a5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857408"
---
# <a name="tutorial-azure-active-directory-integration-with-awardspring"></a><span data-ttu-id="42603-103">Tutorial: Azure Active Directory integration with AwardSpring</span><span class="sxs-lookup"><span data-stu-id="42603-103">Tutorial: Azure Active Directory integration with AwardSpring</span></span>

<span data-ttu-id="42603-104">In this tutorial, you learn how to integrate AwardSpring with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42603-104">In this tutorial, you learn how to integrate AwardSpring with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42603-105">Integrating AwardSpring with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="42603-105">Integrating AwardSpring with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="42603-106">You can control in Azure AD who has access to AwardSpring.</span><span class="sxs-lookup"><span data-stu-id="42603-106">You can control in Azure AD who has access to AwardSpring.</span></span>
- <span data-ttu-id="42603-107">You can enable your users to automatically get signed-on to AwardSpring (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="42603-107">You can enable your users to automatically get signed-on to AwardSpring (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="42603-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="42603-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="42603-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="42603-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42603-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="42603-110">Prerequisites</span></span>

<span data-ttu-id="42603-111">To configure Azure AD integration with AwardSpring, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="42603-111">To configure Azure AD integration with AwardSpring, you need the following items:</span></span>

- <span data-ttu-id="42603-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="42603-112">An Azure AD subscription</span></span>
- <span data-ttu-id="42603-113">An AwardSpring single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="42603-113">An AwardSpring single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42603-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="42603-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42603-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="42603-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42603-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="42603-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="42603-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="42603-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42603-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="42603-118">Scenario description</span></span>
<span data-ttu-id="42603-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="42603-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42603-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="42603-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42603-121">Adding AwardSpring from the gallery</span><span class="sxs-lookup"><span data-stu-id="42603-121">Adding AwardSpring from the gallery</span></span>
1. <span data-ttu-id="42603-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="42603-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-awardspring-from-the-gallery"></a><span data-ttu-id="42603-123">Adding AwardSpring from the gallery</span><span class="sxs-lookup"><span data-stu-id="42603-123">Adding AwardSpring from the gallery</span></span>
<span data-ttu-id="42603-124">To configure the integration of AwardSpring into Azure AD, you need to add AwardSpring from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="42603-124">To configure the integration of AwardSpring into Azure AD, you need to add AwardSpring from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="42603-125">**To add AwardSpring from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="42603-125">**To add AwardSpring from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="42603-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="42603-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="42603-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="42603-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="42603-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="42603-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="42603-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="42603-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="42603-133">In the search box, type **AwardSpring**, select **AwardSpring** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="42603-133">In the search box, type **AwardSpring**, select **AwardSpring** from result panel then click **Add** button to add the application.</span></span>

    ![AwardSpring in the results list](./media/awardspring-tutorial/tutorial_awardspring_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="42603-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="42603-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="42603-136">In this section, you configure and test Azure AD single sign-on with AwardSpring based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="42603-136">In this section, you configure and test Azure AD single sign-on with AwardSpring based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="42603-137">For single sign-on to work, Azure AD needs to know what the counterpart user in AwardSpring is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42603-137">For single sign-on to work, Azure AD needs to know what the counterpart user in AwardSpring is to a user in Azure AD.</span></span> <span data-ttu-id="42603-138">In other words, a link relationship between an Azure AD user and the related user in AwardSpring needs to be established.</span><span class="sxs-lookup"><span data-stu-id="42603-138">In other words, a link relationship between an Azure AD user and the related user in AwardSpring needs to be established.</span></span>

<span data-ttu-id="42603-139">To configure and test Azure AD single sign-on with AwardSpring, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="42603-139">To configure and test Azure AD single sign-on with AwardSpring, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="42603-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="42603-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="42603-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42603-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="42603-142">**[Create an AwardSpring test user](#create-an-awardspring-test-user)** - to have a counterpart of Britta Simon in AwardSpring that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="42603-142">**[Create an AwardSpring test user](#create-an-awardspring-test-user)** - to have a counterpart of Britta Simon in AwardSpring that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="42603-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="42603-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="42603-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="42603-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="42603-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="42603-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="42603-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AwardSpring application.</span><span class="sxs-lookup"><span data-stu-id="42603-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AwardSpring application.</span></span>

<span data-ttu-id="42603-147">**To configure Azure AD single sign-on with AwardSpring, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="42603-147">**To configure Azure AD single sign-on with AwardSpring, perform the following steps:**</span></span>

1. <span data-ttu-id="42603-148">In the Azure portal, on the **AwardSpring** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="42603-148">In the Azure portal, on the **AwardSpring** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="42603-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="42603-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/awardspring-tutorial/tutorial_awardspring_samlbase.png)

1. <span data-ttu-id="42603-152">On the **AwardSpring Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="42603-152">On the **AwardSpring Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![AwardSpring Domain and URLs single sign-on information](./media/awardspring-tutorial/tutorial_awardspring_url.png)

    <span data-ttu-id="42603-154">a.</span><span class="sxs-lookup"><span data-stu-id="42603-154">a.</span></span> <span data-ttu-id="42603-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.awardspring.com/SignIn/SamlMetaData`</span><span class="sxs-lookup"><span data-stu-id="42603-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.awardspring.com/SignIn/SamlMetaData`</span></span>

    <span data-ttu-id="42603-156">b.</span><span class="sxs-lookup"><span data-stu-id="42603-156">b.</span></span> <span data-ttu-id="42603-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.awardspring.com/SignIn/SamlAcs`</span><span class="sxs-lookup"><span data-stu-id="42603-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.awardspring.com/SignIn/SamlAcs`</span></span>

1. <span data-ttu-id="42603-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="42603-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![AwardSpring Domain and URLs single sign-on information](./media/awardspring-tutorial/tutorial_awardspring_url1.png)

    <span data-ttu-id="42603-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.awardspring.com/`</span><span class="sxs-lookup"><span data-stu-id="42603-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.awardspring.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="42603-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="42603-161">These values are not real.</span></span> <span data-ttu-id="42603-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="42603-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="42603-163">Contact [AwardSpring Client support team](mailto:support@awardspring.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="42603-163">Contact [AwardSpring Client support team](mailto:support@awardspring.com) to get these values.</span></span> 

1. <span data-ttu-id="42603-164">AwardSpring application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="42603-164">AwardSpring application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="42603-165">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="42603-165">Configure the following claims for this application.</span></span> <span data-ttu-id="42603-166">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="42603-166">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="42603-167">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="42603-167">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On](./media/awardspring-tutorial/tutorial_awardSpring_attribute.png)

1. <span data-ttu-id="42603-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="42603-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="42603-170">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="42603-170">Attribute Name</span></span> | <span data-ttu-id="42603-171">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="42603-171">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="42603-172">First Name</span><span class="sxs-lookup"><span data-stu-id="42603-172">First Name</span></span> | <span data-ttu-id="42603-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="42603-173">user.givenname</span></span> |
    | <span data-ttu-id="42603-174">Last Name</span><span class="sxs-lookup"><span data-stu-id="42603-174">Last Name</span></span> | <span data-ttu-id="42603-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="42603-175">user.surname</span></span> |
    | <span data-ttu-id="42603-176">Email</span><span class="sxs-lookup"><span data-stu-id="42603-176">Email</span></span> | <span data-ttu-id="42603-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="42603-177">user.mail</span></span> |
    | <span data-ttu-id="42603-178">Username</span><span class="sxs-lookup"><span data-stu-id="42603-178">Username</span></span> | <span data-ttu-id="42603-179">user.userprinicipalname</span><span class="sxs-lookup"><span data-stu-id="42603-179">user.userprinicipalname</span></span> |
    | <span data-ttu-id="42603-180">StudentID</span><span class="sxs-lookup"><span data-stu-id="42603-180">StudentID</span></span> | <span data-ttu-id="42603-181">< Student ID ></span><span class="sxs-lookup"><span data-stu-id="42603-181">< Student ID ></span></span> |

    > [!NOTE]
    > <span data-ttu-id="42603-182">The StudentID attribute is mapped with the actual Student ID which needs to be passed back in claims.</span><span class="sxs-lookup"><span data-stu-id="42603-182">The StudentID attribute is mapped with the actual Student ID which needs to be passed back in claims.</span></span> <span data-ttu-id="42603-183">Contact [AwardSpring Client support team](mailto:support@awardspring.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="42603-183">Contact [AwardSpring Client support team](mailto:support@awardspring.com) to get this value.</span></span>

    <span data-ttu-id="42603-184">a.</span><span class="sxs-lookup"><span data-stu-id="42603-184">a.</span></span> <span data-ttu-id="42603-185">Remove existing attributes and add new attributes.</span><span class="sxs-lookup"><span data-stu-id="42603-185">Remove existing attributes and add new attributes.</span></span> <span data-ttu-id="42603-186">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="42603-186">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/awardspring-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/awardspring-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="42603-189">b.</span><span class="sxs-lookup"><span data-stu-id="42603-189">b.</span></span> <span data-ttu-id="42603-190">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="42603-190">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="42603-191">c.</span><span class="sxs-lookup"><span data-stu-id="42603-191">c.</span></span> <span data-ttu-id="42603-192">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="42603-192">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="42603-193">d.</span><span class="sxs-lookup"><span data-stu-id="42603-193">d.</span></span> <span data-ttu-id="42603-194">Leave the **Namespace** blank.</span><span class="sxs-lookup"><span data-stu-id="42603-194">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="42603-195">d.</span><span class="sxs-lookup"><span data-stu-id="42603-195">d.</span></span> <span data-ttu-id="42603-196">Click **Ok**</span><span class="sxs-lookup"><span data-stu-id="42603-196">Click **Ok**</span></span>

1. <span data-ttu-id="42603-197">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="42603-197">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/awardspring-tutorial/tutorial_awardspring_certificate.png) 

1. <span data-ttu-id="42603-199">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="42603-199">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/awardspring-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="42603-201">To configure single sign-on on **AwardSpring** side, you need to send the downloaded **Metadata XML** to [AwardSpring support team](mailto:support@awardspring.com).</span><span class="sxs-lookup"><span data-stu-id="42603-201">To configure single sign-on on **AwardSpring** side, you need to send the downloaded **Metadata XML** to [AwardSpring support team](mailto:support@awardspring.com).</span></span> <span data-ttu-id="42603-202">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="42603-202">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="42603-203">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="42603-203">Create an Azure AD test user</span></span>

<span data-ttu-id="42603-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42603-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="42603-206">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="42603-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="42603-207">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="42603-207">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/awardspring-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="42603-209">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="42603-209">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/awardspring-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="42603-211">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="42603-211">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/awardspring-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="42603-213">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="42603-213">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/awardspring-tutorial/create_aaduser_04.png)

    <span data-ttu-id="42603-215">a.</span><span class="sxs-lookup"><span data-stu-id="42603-215">a.</span></span> <span data-ttu-id="42603-216">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="42603-216">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42603-217">b.</span><span class="sxs-lookup"><span data-stu-id="42603-217">b.</span></span> <span data-ttu-id="42603-218">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42603-218">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="42603-219">c.</span><span class="sxs-lookup"><span data-stu-id="42603-219">c.</span></span> <span data-ttu-id="42603-220">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="42603-220">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="42603-221">d.</span><span class="sxs-lookup"><span data-stu-id="42603-221">d.</span></span> <span data-ttu-id="42603-222">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="42603-222">Click **Create**.</span></span>
 
### <a name="create-an-awardspring-test-user"></a><span data-ttu-id="42603-223">Create an AwardSpring test user</span><span class="sxs-lookup"><span data-stu-id="42603-223">Create an AwardSpring test user</span></span>

<span data-ttu-id="42603-224">The objective of this section is to create a user called Britta Simon in AwardSpring.</span><span class="sxs-lookup"><span data-stu-id="42603-224">The objective of this section is to create a user called Britta Simon in AwardSpring.</span></span> <span data-ttu-id="42603-225">AwardSpring supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="42603-225">AwardSpring supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="42603-226">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="42603-226">There is no action item for you in this section.</span></span> <span data-ttu-id="42603-227">A new user is created during an attempt to access AwardSpring if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="42603-227">A new user is created during an attempt to access AwardSpring if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="42603-228">If you need to create a user manually, contact [AwardSpring support team](maito:support@awardspring.com).</span><span class="sxs-lookup"><span data-stu-id="42603-228">If you need to create a user manually, contact [AwardSpring support team](maito:support@awardspring.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="42603-229">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="42603-229">Assign the Azure AD test user</span></span>

<span data-ttu-id="42603-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AwardSpring.</span><span class="sxs-lookup"><span data-stu-id="42603-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AwardSpring.</span></span>

![Assign the user role][200] 

<span data-ttu-id="42603-232">**To assign Britta Simon to AwardSpring, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="42603-232">**To assign Britta Simon to AwardSpring, perform the following steps:**</span></span>

1. <span data-ttu-id="42603-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="42603-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="42603-235">In the applications list, select **AwardSpring**.</span><span class="sxs-lookup"><span data-stu-id="42603-235">In the applications list, select **AwardSpring**.</span></span>

    ![The AwardSpring link in the Applications list](./media/awardspring-tutorial/tutorial_awardspring_app.png)  

1. <span data-ttu-id="42603-237">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="42603-237">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="42603-239">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="42603-239">Click **Add** button.</span></span> <span data-ttu-id="42603-240">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="42603-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="42603-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="42603-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="42603-243">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="42603-243">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="42603-244">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="42603-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="42603-245">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="42603-245">Test single sign-on</span></span>

<span data-ttu-id="42603-246">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="42603-246">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="42603-247">When you click the AwardSpring tile in the Access Panel, you should get automatically signed-on to your AwardSpring application.</span><span class="sxs-lookup"><span data-stu-id="42603-247">When you click the AwardSpring tile in the Access Panel, you should get automatically signed-on to your AwardSpring application.</span></span>
<span data-ttu-id="42603-248">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="42603-248">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="42603-249">Additional resources</span><span class="sxs-lookup"><span data-stu-id="42603-249">Additional resources</span></span>

* [<span data-ttu-id="42603-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42603-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="42603-251">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="42603-251">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/awardspring-tutorial/tutorial_general_01.png
[2]: ./media/awardspring-tutorial/tutorial_general_02.png
[3]: ./media/awardspring-tutorial/tutorial_general_03.png
[4]: ./media/awardspring-tutorial/tutorial_general_04.png

[100]: ./media/awardspring-tutorial/tutorial_general_100.png

[200]: ./media/awardspring-tutorial/tutorial_general_200.png
[201]: ./media/awardspring-tutorial/tutorial_general_201.png
[202]: ./media/awardspring-tutorial/tutorial_general_202.png
[203]: ./media/awardspring-tutorial/tutorial_general_203.png

