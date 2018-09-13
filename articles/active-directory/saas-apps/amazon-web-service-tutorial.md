---
title: 'Tutorial: Azure Active Directory integration with Amazon Web Services (AWS) | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Amazon Web Services (AWS).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2018
ms.author: jeedes
ms.openlocfilehash: 8ddcd66d0675603f4e130a9ca367cc4eed7353e7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864345"
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="264ad-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="264ad-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>

<span data-ttu-id="264ad-104">In this tutorial, you learn how to integrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="264ad-104">In this tutorial, you learn how to integrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="264ad-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="264ad-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="264ad-106">You can control in Azure AD who has access to Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="264ad-106">You can control in Azure AD who has access to Amazon Web Services (AWS).</span></span>
- <span data-ttu-id="264ad-107">You can enable your users to automatically get signed-on to Amazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="264ad-107">You can enable your users to automatically get signed-on to Amazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="264ad-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="264ad-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="264ad-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="264ad-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

![Amazon Web Services (AWS)](./media/amazon-web-service-tutorial/tutorial_amazonwebservices(aws)_image.png)

## <a name="prerequisites"></a><span data-ttu-id="264ad-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="264ad-111">Prerequisites</span></span>

<span data-ttu-id="264ad-112">To configure Azure AD integration with Amazon Web Services (AWS), you need the following items:</span><span class="sxs-lookup"><span data-stu-id="264ad-112">To configure Azure AD integration with Amazon Web Services (AWS), you need the following items:</span></span>

- <span data-ttu-id="264ad-113">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="264ad-113">An Azure AD subscription</span></span>
- <span data-ttu-id="264ad-114">An Amazon Web Services (AWS) single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="264ad-114">An Amazon Web Services (AWS) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="264ad-115">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="264ad-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="264ad-116">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="264ad-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="264ad-117">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="264ad-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="264ad-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="264ad-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

> [!Note]
> <span data-ttu-id="264ad-119">If you want to integrate multiple AWS accounts to one Azure account for Single Sign on, please refer [this](https://docs.microsoft.com/azure/active-directory/active-directory-saas-aws-multi-accounts-tutorial) article.</span><span class="sxs-lookup"><span data-stu-id="264ad-119">If you want to integrate multiple AWS accounts to one Azure account for Single Sign on, please refer [this](https://docs.microsoft.com/azure/active-directory/active-directory-saas-aws-multi-accounts-tutorial) article.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="264ad-120">Scenario description</span><span class="sxs-lookup"><span data-stu-id="264ad-120">Scenario description</span></span>

<span data-ttu-id="264ad-121">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="264ad-121">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="264ad-122">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="264ad-122">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="264ad-123">Adding Amazon Web Services (AWS) from the gallery</span><span class="sxs-lookup"><span data-stu-id="264ad-123">Adding Amazon Web Services (AWS) from the gallery</span></span>
2. <span data-ttu-id="264ad-124">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="264ad-124">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-the-gallery"></a><span data-ttu-id="264ad-125">Adding Amazon Web Services (AWS) from the gallery</span><span class="sxs-lookup"><span data-stu-id="264ad-125">Adding Amazon Web Services (AWS) from the gallery</span></span>
<span data-ttu-id="264ad-126">To configure the integration of Amazon Web Services (AWS) into Azure AD, you need to add Amazon Web Services (AWS) from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="264ad-126">To configure the integration of Amazon Web Services (AWS) into Azure AD, you need to add Amazon Web Services (AWS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="264ad-127">**To add Amazon Web Services (AWS) from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="264ad-127">**To add Amazon Web Services (AWS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="264ad-128">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="264ad-128">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="264ad-130">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="264ad-130">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="264ad-131">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="264ad-131">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="264ad-133">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="264ad-133">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="264ad-135">In the search box, type **Amazon Web Services (AWS)**, select **Amazon Web Services (AWS)** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="264ad-135">In the search box, type **Amazon Web Services (AWS)**, select **Amazon Web Services (AWS)** from result panel then click **Add** button to add the application.</span></span>

    ![Amazon Web Services (AWS) in the results list](./media/amazon-web-service-tutorial/tutorial_amazonwebservices(aws)_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="264ad-137">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="264ad-137">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="264ad-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="264ad-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="264ad-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Amazon Web Services (AWS) is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="264ad-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Amazon Web Services (AWS) is to a user in Azure AD.</span></span> <span data-ttu-id="264ad-140">In other words, a link relationship between an Azure AD user and the related user in Amazon Web Services (AWS) needs to be established.</span><span class="sxs-lookup"><span data-stu-id="264ad-140">In other words, a link relationship between an Azure AD user and the related user in Amazon Web Services (AWS) needs to be established.</span></span>

<span data-ttu-id="264ad-141">In Amazon Web Services (AWS), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="264ad-141">In Amazon Web Services (AWS), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="264ad-142">To configure and test Azure AD single sign-on with Amazon Web Services (AWS), you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="264ad-142">To configure and test Azure AD single sign-on with Amazon Web Services (AWS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="264ad-143">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="264ad-143">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="264ad-144">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="264ad-144">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="264ad-145">**[Create an Amazon Web Services (AWS) test user](#create-an-amazon-web-services-aws-test-user)** - to have a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="264ad-145">**[Create an Amazon Web Services (AWS) test user](#create-an-amazon-web-services-aws-test-user)** - to have a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="264ad-146">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="264ad-146">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="264ad-147">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="264ad-147">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="264ad-148">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="264ad-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="264ad-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span><span class="sxs-lookup"><span data-stu-id="264ad-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="264ad-150">**To configure Azure AD single sign-on with Amazon Web Services (AWS), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="264ad-150">**To configure Azure AD single sign-on with Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="264ad-151">In the Azure portal, on the **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="264ad-151">In the Azure portal, on the **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="264ad-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="264ad-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/amazon-web-service-tutorial/tutorial_amazonwebservices(aws)_samlbase.png)

3. <span data-ttu-id="264ad-155">On the **Amazon Web Services (AWS) Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span><span class="sxs-lookup"><span data-stu-id="264ad-155">On the **Amazon Web Services (AWS) Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Amazon Web Services (AWS) Domain and URLs single sign-on information](./media/amazon-web-service-tutorial/tutorial_amazonwebservices(aws)_url.png)

4. <span data-ttu-id="264ad-157">The Amazon Web Services (AWS) Software application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="264ad-157">The Amazon Web Services (AWS) Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="264ad-158">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="264ad-158">Configure the following claims for this application.</span></span> <span data-ttu-id="264ad-159">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="264ad-159">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="264ad-160">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="264ad-160">The following screenshot shows an example for this.</span></span>

    ![Configure Single Sign-On attb](./media/amazon-web-service-tutorial/tutorial_amazonwebservices(aws)_attribute.png)

5. <span data-ttu-id="264ad-162">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="264ad-162">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>

    | <span data-ttu-id="264ad-163">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="264ad-163">Attribute Name</span></span>  | <span data-ttu-id="264ad-164">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="264ad-164">Attribute Value</span></span> | <span data-ttu-id="264ad-165">Namespace</span><span class="sxs-lookup"><span data-stu-id="264ad-165">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="264ad-166">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="264ad-166">RoleSessionName</span></span> | <span data-ttu-id="264ad-167">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="264ad-167">user.userprincipalname</span></span> | https://aws.amazon.com/SAML/Attributes |
    | <span data-ttu-id="264ad-168">Role</span><span class="sxs-lookup"><span data-stu-id="264ad-168">Role</span></span>            | <span data-ttu-id="264ad-169">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="264ad-169">user.assignedroles</span></span> |  https://aws.amazon.com/SAML/Attributes |
    | <span data-ttu-id="264ad-170">SessionDuration</span><span class="sxs-lookup"><span data-stu-id="264ad-170">SessionDuration</span></span>             | <span data-ttu-id="264ad-171">"Provide the value of session duration per your need"</span><span class="sxs-lookup"><span data-stu-id="264ad-171">"Provide the value of session duration per your need"</span></span> |  https://aws.amazon.com/SAML/Attributes |

    >[!TIP]
    ><span data-ttu-id="264ad-172">You need to configure the user provisioning in Azure AD to fetch all the roles from AWS Console.</span><span class="sxs-lookup"><span data-stu-id="264ad-172">You need to configure the user provisioning in Azure AD to fetch all the roles from AWS Console.</span></span> <span data-ttu-id="264ad-173">Refer the provisioning steps below.</span><span class="sxs-lookup"><span data-stu-id="264ad-173">Refer the provisioning steps below.</span></span>

    <span data-ttu-id="264ad-174">a.</span><span class="sxs-lookup"><span data-stu-id="264ad-174">a.</span></span> <span data-ttu-id="264ad-175">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="264ad-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On add](./media/amazon-web-service-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On addattb](./media/amazon-web-service-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="264ad-178">b.</span><span class="sxs-lookup"><span data-stu-id="264ad-178">b.</span></span> <span data-ttu-id="264ad-179">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="264ad-179">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="264ad-180">c.</span><span class="sxs-lookup"><span data-stu-id="264ad-180">c.</span></span> <span data-ttu-id="264ad-181">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="264ad-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="264ad-182">d.</span><span class="sxs-lookup"><span data-stu-id="264ad-182">d.</span></span> <span data-ttu-id="264ad-183">In the **Namespace** textbox, type the namespace value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="264ad-183">In the **Namespace** textbox, type the namespace value shown for that row.</span></span>

    <span data-ttu-id="264ad-184">d.</span><span class="sxs-lookup"><span data-stu-id="264ad-184">d.</span></span> <span data-ttu-id="264ad-185">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="264ad-185">Click **Ok**.</span></span>

6. <span data-ttu-id="264ad-186">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="264ad-186">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/amazon-web-service-tutorial/tutorial_amazonwebservices(aws)_certificate.png)

7. <span data-ttu-id="264ad-188">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="264ad-188">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/amazon-web-service-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="264ad-190">In a different browser window, sign-on to your Amazon Web Services (AWS) company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="264ad-190">In a different browser window, sign-on to your Amazon Web Services (AWS) company site as administrator.</span></span>

9. <span data-ttu-id="264ad-191">Click **AWS Home**.</span><span class="sxs-lookup"><span data-stu-id="264ad-191">Click **AWS Home**.</span></span>

    ![Configure Single Sign-On home][11]

10. <span data-ttu-id="264ad-193">Click **Identity and Access Management**.</span><span class="sxs-lookup"><span data-stu-id="264ad-193">Click **Identity and Access Management**.</span></span>

    ![Configure Single Sign-On Identity][12]

11. <span data-ttu-id="264ad-195">Click **Identity Providers**, and then click **Create Provider**.</span><span class="sxs-lookup"><span data-stu-id="264ad-195">Click **Identity Providers**, and then click **Create Provider**.</span></span>

    ![Configure Single Sign-On Provider][13]

12. <span data-ttu-id="264ad-197">On the **Configure Provider** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="264ad-197">On the **Configure Provider** dialog page, perform the following steps:</span></span>

    ![Configure Single Sign-On dialog][14]

    <span data-ttu-id="264ad-199">a.</span><span class="sxs-lookup"><span data-stu-id="264ad-199">a.</span></span> <span data-ttu-id="264ad-200">As **Provider Type**, select **SAML**.</span><span class="sxs-lookup"><span data-stu-id="264ad-200">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="264ad-201">b.</span><span class="sxs-lookup"><span data-stu-id="264ad-201">b.</span></span> <span data-ttu-id="264ad-202">In the **Provider Name** textbox, type a provider name (for example: *WAAD*).</span><span class="sxs-lookup"><span data-stu-id="264ad-202">In the **Provider Name** textbox, type a provider name (for example: *WAAD*).</span></span>

    <span data-ttu-id="264ad-203">c.</span><span class="sxs-lookup"><span data-stu-id="264ad-203">c.</span></span> <span data-ttu-id="264ad-204">To upload your downloaded **metadata file** from Azure portal, click **Choose File**.</span><span class="sxs-lookup"><span data-stu-id="264ad-204">To upload your downloaded **metadata file** from Azure portal, click **Choose File**.</span></span>

    <span data-ttu-id="264ad-205">d.</span><span class="sxs-lookup"><span data-stu-id="264ad-205">d.</span></span> <span data-ttu-id="264ad-206">Click **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="264ad-206">Click **Next Step**.</span></span>

13. <span data-ttu-id="264ad-207">On the **Verify Provider Information** dialog page, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="264ad-207">On the **Verify Provider Information** dialog page, click **Create**.</span></span>

    ![Configure Single Sign-On Verify][15]

14. <span data-ttu-id="264ad-209">Click **Roles**, and then click **Create role**.</span><span class="sxs-lookup"><span data-stu-id="264ad-209">Click **Roles**, and then click **Create role**.</span></span>

    ![Configure Single Sign-On Roles][16]

15. <span data-ttu-id="264ad-211">On the **Create role** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="264ad-211">On the **Create role** page, perform the following steps:</span></span>  

    ![Configure Single Sign-On Trust][19]

    <span data-ttu-id="264ad-213">a.</span><span class="sxs-lookup"><span data-stu-id="264ad-213">a.</span></span> <span data-ttu-id="264ad-214">Select **SAML 2.0 federation** under **Select type of trusted entity**.</span><span class="sxs-lookup"><span data-stu-id="264ad-214">Select **SAML 2.0 federation** under **Select type of trusted entity**.</span></span>

    <span data-ttu-id="264ad-215">b.</span><span class="sxs-lookup"><span data-stu-id="264ad-215">b.</span></span> <span data-ttu-id="264ad-216">Under **Choose a SAML 2.0 Provider section**, select the **SAML provider** you have created previously (for example: *WAAD*)</span><span class="sxs-lookup"><span data-stu-id="264ad-216">Under **Choose a SAML 2.0 Provider section**, select the **SAML provider** you have created previously (for example: *WAAD*)</span></span>

    <span data-ttu-id="264ad-217">c.</span><span class="sxs-lookup"><span data-stu-id="264ad-217">c.</span></span> <span data-ttu-id="264ad-218">Select **Allow programmatic and AWS Management Console access**.</span><span class="sxs-lookup"><span data-stu-id="264ad-218">Select **Allow programmatic and AWS Management Console access**.</span></span>
  
    <span data-ttu-id="264ad-219">d.</span><span class="sxs-lookup"><span data-stu-id="264ad-219">d.</span></span> <span data-ttu-id="264ad-220">Click **Next: Permissions**.</span><span class="sxs-lookup"><span data-stu-id="264ad-220">Click **Next: Permissions**.</span></span>

16. <span data-ttu-id="264ad-221">On the **Attach Permissions Policies** dialog, you don't need to attach any policy.</span><span class="sxs-lookup"><span data-stu-id="264ad-221">On the **Attach Permissions Policies** dialog, you don't need to attach any policy.</span></span> <span data-ttu-id="264ad-222">Click **Next: Review**.</span><span class="sxs-lookup"><span data-stu-id="264ad-222">Click **Next: Review**.</span></span>  

    ![Configure Single Sign-On Policy][33]

17. <span data-ttu-id="264ad-224">On the **Review** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="264ad-224">On the **Review** dialog, perform the following steps:</span></span>

    ![Configure Single Sign-On Review][34]

    <span data-ttu-id="264ad-226">a.</span><span class="sxs-lookup"><span data-stu-id="264ad-226">a.</span></span> <span data-ttu-id="264ad-227">In the **Role name** textbox, enter your Role name.</span><span class="sxs-lookup"><span data-stu-id="264ad-227">In the **Role name** textbox, enter your Role name.</span></span>

    <span data-ttu-id="264ad-228">b.</span><span class="sxs-lookup"><span data-stu-id="264ad-228">b.</span></span> <span data-ttu-id="264ad-229">In the **Role description** textbox, enter the description.</span><span class="sxs-lookup"><span data-stu-id="264ad-229">In the **Role description** textbox, enter the description.</span></span>

    <span data-ttu-id="264ad-230">c.</span><span class="sxs-lookup"><span data-stu-id="264ad-230">c.</span></span> <span data-ttu-id="264ad-231">Click **Create Role**.</span><span class="sxs-lookup"><span data-stu-id="264ad-231">Click **Create Role**.</span></span>

    <span data-ttu-id="264ad-232">d.</span><span class="sxs-lookup"><span data-stu-id="264ad-232">d.</span></span> <span data-ttu-id="264ad-233">Create as many roles as needed and map them to the Identity Provider.</span><span class="sxs-lookup"><span data-stu-id="264ad-233">Create as many roles as needed and map them to the Identity Provider.</span></span>

18. <span data-ttu-id="264ad-234">Use AWS service account credentials for fetching the roles from AWS account in Azure AD User Provisioning.</span><span class="sxs-lookup"><span data-stu-id="264ad-234">Use AWS service account credentials for fetching the roles from AWS account in Azure AD User Provisioning.</span></span> <span data-ttu-id="264ad-235">For this, open the AWS console home.</span><span class="sxs-lookup"><span data-stu-id="264ad-235">For this, open the AWS console home.</span></span>

19. <span data-ttu-id="264ad-236">Click on **Services** -> **Security, Identity& Compliance** -> **IAM**.</span><span class="sxs-lookup"><span data-stu-id="264ad-236">Click on **Services** -> **Security, Identity& Compliance** -> **IAM**.</span></span>

    ![fetching the roles from AWS account](./media/amazon-web-service-tutorial/fetchingrole1.png)

20. <span data-ttu-id="264ad-238">Select the **Policies** tab in the IAM section.</span><span class="sxs-lookup"><span data-stu-id="264ad-238">Select the **Policies** tab in the IAM section.</span></span>

    ![fetching the roles from AWS account](./media/amazon-web-service-tutorial/fetchingrole2.png)

21. <span data-ttu-id="264ad-240">Create a new policy by clicking on **Create policy** for fetching the roles from AWS account in Azure AD User Provisioning.</span><span class="sxs-lookup"><span data-stu-id="264ad-240">Create a new policy by clicking on **Create policy** for fetching the roles from AWS account in Azure AD User Provisioning.</span></span>

    ![Creating new policy](./media/amazon-web-service-tutorial/fetchingrole3.png)

22. <span data-ttu-id="264ad-242">Create your own policy to fetch all the roles from AWS accounts by performing the following steps:</span><span class="sxs-lookup"><span data-stu-id="264ad-242">Create your own policy to fetch all the roles from AWS accounts by performing the following steps:</span></span>

    ![Creating new policy](./media/amazon-web-service-tutorial/policy1.png)

    <span data-ttu-id="264ad-244">a.</span><span class="sxs-lookup"><span data-stu-id="264ad-244">a.</span></span> <span data-ttu-id="264ad-245">In the **“Create policy”** section click on **“JSON”** tab.</span><span class="sxs-lookup"><span data-stu-id="264ad-245">In the **“Create policy”** section click on **“JSON”** tab.</span></span>

    <span data-ttu-id="264ad-246">b.</span><span class="sxs-lookup"><span data-stu-id="264ad-246">b.</span></span> <span data-ttu-id="264ad-247">In the policy document, add the below JSON.</span><span class="sxs-lookup"><span data-stu-id="264ad-247">In the policy document, add the below JSON.</span></span>

    ```

    {

    "Version": "2012-10-17",

    "Statement": [

    {

    "Effect": "Allow",

    "Action": [

    "iam:ListRoles"

    ],

    "Resource": "*"

    }

    ]

    }

    ```

    <span data-ttu-id="264ad-248">c.</span><span class="sxs-lookup"><span data-stu-id="264ad-248">c.</span></span> <span data-ttu-id="264ad-249">Click on **Review Policy button** to validate the policy.</span><span class="sxs-lookup"><span data-stu-id="264ad-249">Click on **Review Policy button** to validate the policy.</span></span>

    ![Define the new policy](./media/amazon-web-service-tutorial/policy5.png)

23. <span data-ttu-id="264ad-251">Define the **new policy** by performing the following steps:</span><span class="sxs-lookup"><span data-stu-id="264ad-251">Define the **new policy** by performing the following steps:</span></span>

    ![Define the new policy](./media/amazon-web-service-tutorial/policy2.png)

    <span data-ttu-id="264ad-253">a.</span><span class="sxs-lookup"><span data-stu-id="264ad-253">a.</span></span> <span data-ttu-id="264ad-254">Provide the **Policy Name** as **AzureAD_SSOUserRole_Policy**.</span><span class="sxs-lookup"><span data-stu-id="264ad-254">Provide the **Policy Name** as **AzureAD_SSOUserRole_Policy**.</span></span>

    <span data-ttu-id="264ad-255">b.</span><span class="sxs-lookup"><span data-stu-id="264ad-255">b.</span></span> <span data-ttu-id="264ad-256">You can provide **Description** to the policy as **This policy will allow to fetch the roles from AWS accounts**.</span><span class="sxs-lookup"><span data-stu-id="264ad-256">You can provide **Description** to the policy as **This policy will allow to fetch the roles from AWS accounts**.</span></span>

    <span data-ttu-id="264ad-257">c.</span><span class="sxs-lookup"><span data-stu-id="264ad-257">c.</span></span> <span data-ttu-id="264ad-258">Click on **“Create Policy”** button.</span><span class="sxs-lookup"><span data-stu-id="264ad-258">Click on **“Create Policy”** button.</span></span>

24. <span data-ttu-id="264ad-259">Create a new user account in the AWS IAM Service by performing the following steps:</span><span class="sxs-lookup"><span data-stu-id="264ad-259">Create a new user account in the AWS IAM Service by performing the following steps:</span></span>

    <span data-ttu-id="264ad-260">a.</span><span class="sxs-lookup"><span data-stu-id="264ad-260">a.</span></span> <span data-ttu-id="264ad-261">Click on **Users** navigation in the AWS IAM console.</span><span class="sxs-lookup"><span data-stu-id="264ad-261">Click on **Users** navigation in the AWS IAM console.</span></span>

    ![Define the new policy](./media/amazon-web-service-tutorial/policy3.png)

    <span data-ttu-id="264ad-263">b.</span><span class="sxs-lookup"><span data-stu-id="264ad-263">b.</span></span> <span data-ttu-id="264ad-264">Click on **Add user** button to create a new user.</span><span class="sxs-lookup"><span data-stu-id="264ad-264">Click on **Add user** button to create a new user.</span></span>

    ![Add user](./media/amazon-web-service-tutorial/policy4.png)

    <span data-ttu-id="264ad-266">c.</span><span class="sxs-lookup"><span data-stu-id="264ad-266">c.</span></span> <span data-ttu-id="264ad-267">In the **Add user** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="264ad-267">In the **Add user** section, perform the following steps:</span></span>

    ![Add user](./media/amazon-web-service-tutorial/adduser1.png)

    * <span data-ttu-id="264ad-269">Enter the user name as **AzureADRoleManager**.</span><span class="sxs-lookup"><span data-stu-id="264ad-269">Enter the user name as **AzureADRoleManager**.</span></span>

    * <span data-ttu-id="264ad-270">In the Access type, select the **Programmatic access** option.</span><span class="sxs-lookup"><span data-stu-id="264ad-270">In the Access type, select the **Programmatic access** option.</span></span> <span data-ttu-id="264ad-271">This way the user can invoke the APIs and fetch the roles from AWS account.</span><span class="sxs-lookup"><span data-stu-id="264ad-271">This way the user can invoke the APIs and fetch the roles from AWS account.</span></span>

    * <span data-ttu-id="264ad-272">Click on the **Next Permissions** button in the bottom right corner.</span><span class="sxs-lookup"><span data-stu-id="264ad-272">Click on the **Next Permissions** button in the bottom right corner.</span></span>

25. <span data-ttu-id="264ad-273">Now create a new policy for this user by performing the following steps:</span><span class="sxs-lookup"><span data-stu-id="264ad-273">Now create a new policy for this user by performing the following steps:</span></span>

    ![Add user](./media/amazon-web-service-tutorial/adduser2.png)

    <span data-ttu-id="264ad-275">a.</span><span class="sxs-lookup"><span data-stu-id="264ad-275">a.</span></span> <span data-ttu-id="264ad-276">Click on the **Attach existing policies directly** button.</span><span class="sxs-lookup"><span data-stu-id="264ad-276">Click on the **Attach existing policies directly** button.</span></span>

    <span data-ttu-id="264ad-277">b.</span><span class="sxs-lookup"><span data-stu-id="264ad-277">b.</span></span> <span data-ttu-id="264ad-278">Search for the newly created policy in the filter section **AzureAD_SSOUserRole_Policy**.</span><span class="sxs-lookup"><span data-stu-id="264ad-278">Search for the newly created policy in the filter section **AzureAD_SSOUserRole_Policy**.</span></span>

    <span data-ttu-id="264ad-279">c.</span><span class="sxs-lookup"><span data-stu-id="264ad-279">c.</span></span> <span data-ttu-id="264ad-280">Select the **policy** and then click on the **Next: Review** button.</span><span class="sxs-lookup"><span data-stu-id="264ad-280">Select the **policy** and then click on the **Next: Review** button.</span></span>

26. <span data-ttu-id="264ad-281">Review the policy to the attached user by performing following steps:</span><span class="sxs-lookup"><span data-stu-id="264ad-281">Review the policy to the attached user by performing following steps:</span></span>

    ![Add user](./media/amazon-web-service-tutorial/adduser3.png)

    <span data-ttu-id="264ad-283">a.</span><span class="sxs-lookup"><span data-stu-id="264ad-283">a.</span></span> <span data-ttu-id="264ad-284">Review the user name, access type, and policy mapped to the user.</span><span class="sxs-lookup"><span data-stu-id="264ad-284">Review the user name, access type, and policy mapped to the user.</span></span>

    <span data-ttu-id="264ad-285">b.</span><span class="sxs-lookup"><span data-stu-id="264ad-285">b.</span></span> <span data-ttu-id="264ad-286">Click on the **Create user** button at the bottom right corner to create the user.</span><span class="sxs-lookup"><span data-stu-id="264ad-286">Click on the **Create user** button at the bottom right corner to create the user.</span></span>

27. <span data-ttu-id="264ad-287">Download the user credentials of a user by performing following steps:</span><span class="sxs-lookup"><span data-stu-id="264ad-287">Download the user credentials of a user by performing following steps:</span></span>

    ![Add user](./media/amazon-web-service-tutorial/adduser4.png)

    <span data-ttu-id="264ad-289">a.</span><span class="sxs-lookup"><span data-stu-id="264ad-289">a.</span></span> <span data-ttu-id="264ad-290">Copy the user **Access key ID** and **Secret access key**.</span><span class="sxs-lookup"><span data-stu-id="264ad-290">Copy the user **Access key ID** and **Secret access key**.</span></span>

    <span data-ttu-id="264ad-291">b.</span><span class="sxs-lookup"><span data-stu-id="264ad-291">b.</span></span> <span data-ttu-id="264ad-292">Enter these credentials into Azure AD user provisioning section to fetch the roles from AWS console.</span><span class="sxs-lookup"><span data-stu-id="264ad-292">Enter these credentials into Azure AD user provisioning section to fetch the roles from AWS console.</span></span>

    <span data-ttu-id="264ad-293">c.</span><span class="sxs-lookup"><span data-stu-id="264ad-293">c.</span></span> <span data-ttu-id="264ad-294">Click on **Close** button at the bottom.</span><span class="sxs-lookup"><span data-stu-id="264ad-294">Click on **Close** button at the bottom.</span></span>

28. <span data-ttu-id="264ad-295">Navigate to **User Provisioning** section of Amazon Web Services app in Azure AD Management Portal.</span><span class="sxs-lookup"><span data-stu-id="264ad-295">Navigate to **User Provisioning** section of Amazon Web Services app in Azure AD Management Portal.</span></span>

    ![Add user](./media/amazon-web-service-tutorial/provisioning.png)

29. <span data-ttu-id="264ad-297">Enter the **Access Key** and **Secret** in the **Client Secret** and **Secret Token** field respectively.</span><span class="sxs-lookup"><span data-stu-id="264ad-297">Enter the **Access Key** and **Secret** in the **Client Secret** and **Secret Token** field respectively.</span></span>

    ![Add user](./media/amazon-web-service-tutorial/provisioning1.png)

    <span data-ttu-id="264ad-299">a.</span><span class="sxs-lookup"><span data-stu-id="264ad-299">a.</span></span> <span data-ttu-id="264ad-300">Enter the AWS user access key in the **clientsecret** field.</span><span class="sxs-lookup"><span data-stu-id="264ad-300">Enter the AWS user access key in the **clientsecret** field.</span></span>

    <span data-ttu-id="264ad-301">b.</span><span class="sxs-lookup"><span data-stu-id="264ad-301">b.</span></span> <span data-ttu-id="264ad-302">Enter the AWS user secret in the **Secret Token** field.</span><span class="sxs-lookup"><span data-stu-id="264ad-302">Enter the AWS user secret in the **Secret Token** field.</span></span>

    <span data-ttu-id="264ad-303">c.</span><span class="sxs-lookup"><span data-stu-id="264ad-303">c.</span></span> <span data-ttu-id="264ad-304">Click on the **Test Connection** button and you should able to successfully test this connection.</span><span class="sxs-lookup"><span data-stu-id="264ad-304">Click on the **Test Connection** button and you should able to successfully test this connection.</span></span>

    <span data-ttu-id="264ad-305">d.</span><span class="sxs-lookup"><span data-stu-id="264ad-305">d.</span></span> <span data-ttu-id="264ad-306">Save the setting by clicking on the **Save** button at the top.</span><span class="sxs-lookup"><span data-stu-id="264ad-306">Save the setting by clicking on the **Save** button at the top.</span></span>

30. <span data-ttu-id="264ad-307">Now make sure that you enable the Provisioning Status **On** in the Settings section by making the switch on and then clicking on the **Save** button at the top.</span><span class="sxs-lookup"><span data-stu-id="264ad-307">Now make sure that you enable the Provisioning Status **On** in the Settings section by making the switch on and then clicking on the **Save** button at the top.</span></span>

    ![Add user](./media/amazon-web-service-tutorial/provisioning2.png)

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="264ad-309">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="264ad-309">Create an Azure AD test user</span></span>

<span data-ttu-id="264ad-310">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="264ad-310">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="264ad-312">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="264ad-312">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="264ad-313">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="264ad-313">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/amazon-web-service-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="264ad-315">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="264ad-315">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/amazon-web-service-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="264ad-317">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="264ad-317">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/amazon-web-service-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="264ad-319">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="264ad-319">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/amazon-web-service-tutorial/create_aaduser_04.png)

    <span data-ttu-id="264ad-321">a.</span><span class="sxs-lookup"><span data-stu-id="264ad-321">a.</span></span> <span data-ttu-id="264ad-322">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="264ad-322">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="264ad-323">b.</span><span class="sxs-lookup"><span data-stu-id="264ad-323">b.</span></span> <span data-ttu-id="264ad-324">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="264ad-324">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="264ad-325">c.</span><span class="sxs-lookup"><span data-stu-id="264ad-325">c.</span></span> <span data-ttu-id="264ad-326">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="264ad-326">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="264ad-327">d.</span><span class="sxs-lookup"><span data-stu-id="264ad-327">d.</span></span> <span data-ttu-id="264ad-328">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="264ad-328">Click **Create**.</span></span>

### <a name="create-an-amazon-web-services-aws-test-user"></a><span data-ttu-id="264ad-329">Create an Amazon Web Services (AWS) test user</span><span class="sxs-lookup"><span data-stu-id="264ad-329">Create an Amazon Web Services (AWS) test user</span></span>

<span data-ttu-id="264ad-330">The objective of this section is to create a user called Britta Simon in Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="264ad-330">The objective of this section is to create a user called Britta Simon in Amazon Web Services (AWS).</span></span> <span data-ttu-id="264ad-331">Amazon Web Services (AWS) doesn't need a user to be created in their system for SSO, so you don't need to perform any action here.</span><span class="sxs-lookup"><span data-stu-id="264ad-331">Amazon Web Services (AWS) doesn't need a user to be created in their system for SSO, so you don't need to perform any action here.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="264ad-332">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="264ad-332">Assign the Azure AD test user</span></span>

<span data-ttu-id="264ad-333">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="264ad-333">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Amazon Web Services (AWS).</span></span>

![Assign the user role][200]

<span data-ttu-id="264ad-335">**To assign Britta Simon to Amazon Web Services (AWS), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="264ad-335">**To assign Britta Simon to Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="264ad-336">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="264ad-336">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="264ad-338">In the applications list, select **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="264ad-338">In the applications list, select **Amazon Web Services (AWS)**.</span></span>

    ![The Amazon Web Services (AWS) link in the Applications list](./media/amazon-web-service-tutorial/tutorial_amazonwebservices(aws)_app.png)  

3. <span data-ttu-id="264ad-340">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="264ad-340">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="264ad-342">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="264ad-342">Click **Add** button.</span></span> <span data-ttu-id="264ad-343">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="264ad-343">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="264ad-345">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="264ad-345">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="264ad-346">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="264ad-346">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="264ad-347">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="264ad-347">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="264ad-348">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="264ad-348">Test single sign-on</span></span>

<span data-ttu-id="264ad-349">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="264ad-349">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="264ad-350">When you click the Amazon Web Services (AWS) tile in the Access Panel, you should get automatically signed-on to your Amazon Web Services (AWS) application.</span><span class="sxs-lookup"><span data-stu-id="264ad-350">When you click the Amazon Web Services (AWS) tile in the Access Panel, you should get automatically signed-on to your Amazon Web Services (AWS) application.</span></span>
<span data-ttu-id="264ad-351">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="264ad-351">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="264ad-352">Additional resources</span><span class="sxs-lookup"><span data-stu-id="264ad-352">Additional resources</span></span>

* [<span data-ttu-id="264ad-353">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="264ad-353">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="264ad-354">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="264ad-354">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/amazon-web-service-tutorial/ic795031.png
[12]: ./media/amazon-web-service-tutorial/ic795032.png
[13]: ./media/amazon-web-service-tutorial/ic795033.png
[14]: ./media/amazon-web-service-tutorial/ic795034.png
[15]: ./media/amazon-web-service-tutorial/ic795035.png
[16]: ./media/amazon-web-service-tutorial/ic795022.png
[17]: ./media/amazon-web-service-tutorial/ic795023.png
[18]: ./media/amazon-web-service-tutorial/ic795024.png
[19]: ./media/amazon-web-service-tutorial/ic795025.png
[32]: ./media/amazon-web-service-tutorial/ic7950251.png
[33]: ./media/amazon-web-service-tutorial/ic7950252.png
[35]: ./media/amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[34]: ./media/amazon-web-service-tutorial/ic7950253.png
[36]: ./media/amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png

