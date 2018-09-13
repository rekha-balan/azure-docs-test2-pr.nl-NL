---
title: 'Tutorial: Azure Active Directory integration with Amazon Web Services (AWS) to connect multiple accounts | Microsoft Docs'
description: Learn how to configure single sign-on between Azure AD and multiple accounts of Amazon Web Services (AWS).
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
ms.openlocfilehash: a7d77df4d6be1572d2076684cfa4702cb32b5ed6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856574"
---
# <a name="tutorial-azure-active-directory-integration-with-multiple-amazon-web-services-aws-accounts"></a><span data-ttu-id="8851e-103">Tutorial: Azure Active Directory integration with multiple Amazon Web Services (AWS) accounts</span><span class="sxs-lookup"><span data-stu-id="8851e-103">Tutorial: Azure Active Directory integration with multiple Amazon Web Services (AWS) accounts</span></span>

<span data-ttu-id="8851e-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with multiple accounts of Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="8851e-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with multiple accounts of Amazon Web Services (AWS).</span></span>

<span data-ttu-id="8851e-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8851e-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8851e-106">You can control in Azure AD who has access to Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="8851e-106">You can control in Azure AD who has access to Amazon Web Services (AWS).</span></span>
- <span data-ttu-id="8851e-107">You can enable your users to automatically get signed-on to Amazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="8851e-107">You can enable your users to automatically get signed-on to Amazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8851e-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8851e-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="8851e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="8851e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

![Amazon Web Services (AWS) in the results list](./media/aws-multi-accounts-tutorial/amazonwebservice.png)

## <a name="prerequisites"></a><span data-ttu-id="8851e-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8851e-111">Prerequisites</span></span>

<span data-ttu-id="8851e-112">To configure Azure AD integration with Amazon Web Services (AWS), you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8851e-112">To configure Azure AD integration with Amazon Web Services (AWS), you need the following items:</span></span>

- <span data-ttu-id="8851e-113">An Azure AD basic or premium subscription</span><span class="sxs-lookup"><span data-stu-id="8851e-113">An Azure AD basic or premium subscription</span></span>
- <span data-ttu-id="8851e-114">Amazon Web Services (AWS) multiple single sign-on enabled accounts</span><span class="sxs-lookup"><span data-stu-id="8851e-114">Amazon Web Services (AWS) multiple single sign-on enabled accounts</span></span>

> [!NOTE]
> <span data-ttu-id="8851e-115">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8851e-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8851e-116">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8851e-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8851e-117">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="8851e-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8851e-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8851e-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8851e-119">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8851e-119">Scenario description</span></span>
<span data-ttu-id="8851e-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8851e-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8851e-121">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8851e-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8851e-122">Adding Amazon Web Services (AWS) from the gallery</span><span class="sxs-lookup"><span data-stu-id="8851e-122">Adding Amazon Web Services (AWS) from the gallery</span></span>
2. <span data-ttu-id="8851e-123">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8851e-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-the-gallery"></a><span data-ttu-id="8851e-124">Adding Amazon Web Services (AWS) from the gallery</span><span class="sxs-lookup"><span data-stu-id="8851e-124">Adding Amazon Web Services (AWS) from the gallery</span></span>
<span data-ttu-id="8851e-125">To configure the integration of Amazon Web Services (AWS) into Azure AD, you need to add Amazon Web Services (AWS) from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8851e-125">To configure the integration of Amazon Web Services (AWS) into Azure AD, you need to add Amazon Web Services (AWS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8851e-126">**To add Amazon Web Services (AWS) from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8851e-126">**To add Amazon Web Services (AWS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8851e-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8851e-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="8851e-129">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="8851e-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8851e-130">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8851e-130">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="8851e-132">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="8851e-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="8851e-134">In the search box, type **Amazon Web Services (AWS)**, select **Amazon Web Services (AWS)** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="8851e-134">In the search box, type **Amazon Web Services (AWS)**, select **Amazon Web Services (AWS)** from result panel then click **Add** button to add the application.</span></span>

    ![Amazon Web Services (AWS) in the results list](./media/aws-multi-accounts-tutorial/tutorial_amazonwebservices(aws)_addfromgallery.png)

5. <span data-ttu-id="8851e-136">Once the application is added, go to **Properties** page and copy the **Object ID**.</span><span class="sxs-lookup"><span data-stu-id="8851e-136">Once the application is added, go to **Properties** page and copy the **Object ID**.</span></span>

    ![Amazon Web Services (AWS) in the results list](./media/aws-multi-accounts-tutorial/tutorial_amazonwebservices(aws)_properties.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8851e-138">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8851e-138">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8851e-139">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8851e-139">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8851e-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Amazon Web Services (AWS) is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8851e-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Amazon Web Services (AWS) is to a user in Azure AD.</span></span> <span data-ttu-id="8851e-141">In other words, a link relationship between an Azure AD user and the related user in Amazon Web Services (AWS) needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8851e-141">In other words, a link relationship between an Azure AD user and the related user in Amazon Web Services (AWS) needs to be established.</span></span>

<span data-ttu-id="8851e-142">In Amazon Web Services (AWS), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="8851e-142">In Amazon Web Services (AWS), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8851e-143">To configure and test Azure AD single sign-on with Amazon Web Services (AWS), you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8851e-143">To configure and test Azure AD single sign-on with Amazon Web Services (AWS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8851e-144">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8851e-144">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8851e-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8851e-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8851e-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8851e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8851e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span><span class="sxs-lookup"><span data-stu-id="8851e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="8851e-148">**To configure Azure AD single sign-on with Amazon Web Services (AWS), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8851e-148">**To configure Azure AD single sign-on with Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="8851e-149">In the Azure portal, on the **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8851e-149">In the Azure portal, on the **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="8851e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8851e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/aws-multi-accounts-tutorial/tutorial_amazonwebservices(aws)_samlbase.png)

3. <span data-ttu-id="8851e-153">On the **Amazon Web Services (AWS) Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span><span class="sxs-lookup"><span data-stu-id="8851e-153">On the **Amazon Web Services (AWS) Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Amazon Web Services (AWS) Domain and URLs single sign-on information](./media/aws-multi-accounts-tutorial/tutorial_amazonwebservices(aws)_url.png)

4. <span data-ttu-id="8851e-155">The Amazon Web Services (AWS) Software application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="8851e-155">The Amazon Web Services (AWS) Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="8851e-156">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="8851e-156">Configure the following claims for this application.</span></span> <span data-ttu-id="8851e-157">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="8851e-157">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="8851e-158">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="8851e-158">The following screenshot shows an example for this.</span></span>

    ![Configure Single Sign-On attribute](./media/aws-multi-accounts-tutorial/tutorial_amazonwebservices(aws)_attribute.png)    

5. <span data-ttu-id="8851e-160">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8851e-160">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>

    | <span data-ttu-id="8851e-161">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="8851e-161">Attribute Name</span></span>  | <span data-ttu-id="8851e-162">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="8851e-162">Attribute Value</span></span> | <span data-ttu-id="8851e-163">Namespace</span><span class="sxs-lookup"><span data-stu-id="8851e-163">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="8851e-164">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="8851e-164">RoleSessionName</span></span> | <span data-ttu-id="8851e-165">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="8851e-165">user.userprincipalname</span></span> | https://aws.amazon.com/SAML/Attributes |
    | <span data-ttu-id="8851e-166">Role</span><span class="sxs-lookup"><span data-stu-id="8851e-166">Role</span></span>            | <span data-ttu-id="8851e-167">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="8851e-167">user.assignedroles</span></span> |  https://aws.amazon.com/SAML/Attributes |
    | <span data-ttu-id="8851e-168">SessionDuration</span><span class="sxs-lookup"><span data-stu-id="8851e-168">SessionDuration</span></span>             | <span data-ttu-id="8851e-169">"Provide the value of session duration per your need"</span><span class="sxs-lookup"><span data-stu-id="8851e-169">"Provide the value of session duration per your need"</span></span> |  https://aws.amazon.com/SAML/Attributes |

    >[!TIP]
    ><span data-ttu-id="8851e-170">You need to configure the user provisioning in Azure AD to fetch all the roles from AWS Console.</span><span class="sxs-lookup"><span data-stu-id="8851e-170">You need to configure the user provisioning in Azure AD to fetch all the roles from AWS Console.</span></span> <span data-ttu-id="8851e-171">Refer the provisioning steps below.</span><span class="sxs-lookup"><span data-stu-id="8851e-171">Refer the provisioning steps below.</span></span>

    <span data-ttu-id="8851e-172">a.</span><span class="sxs-lookup"><span data-stu-id="8851e-172">a.</span></span> <span data-ttu-id="8851e-173">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="8851e-173">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On add](./media/aws-multi-accounts-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On attribute](./media/aws-multi-accounts-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="8851e-176">b.</span><span class="sxs-lookup"><span data-stu-id="8851e-176">b.</span></span> <span data-ttu-id="8851e-177">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="8851e-177">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="8851e-178">c.</span><span class="sxs-lookup"><span data-stu-id="8851e-178">c.</span></span> <span data-ttu-id="8851e-179">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="8851e-179">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="8851e-180">d.</span><span class="sxs-lookup"><span data-stu-id="8851e-180">d.</span></span> <span data-ttu-id="8851e-181">In the **Namespace** textbox, type the namespace value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="8851e-181">In the **Namespace** textbox, type the namespace value shown for that row.</span></span>

    <span data-ttu-id="8851e-182">d.</span><span class="sxs-lookup"><span data-stu-id="8851e-182">d.</span></span> <span data-ttu-id="8851e-183">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="8851e-183">Click **Ok**.</span></span>

6. <span data-ttu-id="8851e-184">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8851e-184">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/aws-multi-accounts-tutorial/tutorial_amazonwebservices(aws)_certificate.png) 

7. <span data-ttu-id="8851e-186">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="8851e-186">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/aws-multi-accounts-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8851e-188">In a different browser window, sign-on to your Amazon Web Services (AWS) company site as Administrator.</span><span class="sxs-lookup"><span data-stu-id="8851e-188">In a different browser window, sign-on to your Amazon Web Services (AWS) company site as Administrator.</span></span>

9. <span data-ttu-id="8851e-189">Click **AWS Home**.</span><span class="sxs-lookup"><span data-stu-id="8851e-189">Click **AWS Home**.</span></span>

    ![Configure Single Sign-On home][11]

10. <span data-ttu-id="8851e-191">Click **IAM** (Identity and Access Management).</span><span class="sxs-lookup"><span data-stu-id="8851e-191">Click **IAM** (Identity and Access Management).</span></span>

    ![Configure Single Sign-On Identity][12]

11. <span data-ttu-id="8851e-193">Click **Identity Providers**, and then click **Create Provider**.</span><span class="sxs-lookup"><span data-stu-id="8851e-193">Click **Identity Providers**, and then click **Create Provider**.</span></span>

    ![Configure Single Sign-On Provider][13]

12. <span data-ttu-id="8851e-195">On the **Configure Provider** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8851e-195">On the **Configure Provider** dialog page, perform the following steps:</span></span>

    ![Configure Single Sign-On dialog][14]

    <span data-ttu-id="8851e-197">a.</span><span class="sxs-lookup"><span data-stu-id="8851e-197">a.</span></span> <span data-ttu-id="8851e-198">As **Provider Type**, select **SAML**.</span><span class="sxs-lookup"><span data-stu-id="8851e-198">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="8851e-199">b.</span><span class="sxs-lookup"><span data-stu-id="8851e-199">b.</span></span> <span data-ttu-id="8851e-200">In the **Provider Name** textbox, type a provider name (for example: *WAAD*).</span><span class="sxs-lookup"><span data-stu-id="8851e-200">In the **Provider Name** textbox, type a provider name (for example: *WAAD*).</span></span>

    <span data-ttu-id="8851e-201">c.</span><span class="sxs-lookup"><span data-stu-id="8851e-201">c.</span></span> <span data-ttu-id="8851e-202">To upload your downloaded **metadata file** from Azure portal, click **Choose File**.</span><span class="sxs-lookup"><span data-stu-id="8851e-202">To upload your downloaded **metadata file** from Azure portal, click **Choose File**.</span></span>

    <span data-ttu-id="8851e-203">d.</span><span class="sxs-lookup"><span data-stu-id="8851e-203">d.</span></span> <span data-ttu-id="8851e-204">Click **Next Step**.</span><span class="sxs-lookup"><span data-stu-id="8851e-204">Click **Next Step**.</span></span>

13. <span data-ttu-id="8851e-205">On the **Verify Provider Information** dialog page, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8851e-205">On the **Verify Provider Information** dialog page, click **Create**.</span></span>

    ![Configure Single Sign-On Verify][15]

14. <span data-ttu-id="8851e-207">Click **Roles**, and then click **Create role**.</span><span class="sxs-lookup"><span data-stu-id="8851e-207">Click **Roles**, and then click **Create role**.</span></span>

    ![Configure Single Sign-On Roles][16]

15. <span data-ttu-id="8851e-209">On the **Create role** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8851e-209">On the **Create role** page, perform the following steps:</span></span>  

    ![Configure Single Sign-On Trust][19]

    <span data-ttu-id="8851e-211">a.</span><span class="sxs-lookup"><span data-stu-id="8851e-211">a.</span></span> <span data-ttu-id="8851e-212">Select **SAML 2.0 federation** under **Select type of trusted entity**.</span><span class="sxs-lookup"><span data-stu-id="8851e-212">Select **SAML 2.0 federation** under **Select type of trusted entity**.</span></span>

    <span data-ttu-id="8851e-213">b.</span><span class="sxs-lookup"><span data-stu-id="8851e-213">b.</span></span> <span data-ttu-id="8851e-214">Under **Choose a SAML 2.0 Provider section**, select the **SAML provider** you have created previously (for example: *WAAD*)</span><span class="sxs-lookup"><span data-stu-id="8851e-214">Under **Choose a SAML 2.0 Provider section**, select the **SAML provider** you have created previously (for example: *WAAD*)</span></span>

    <span data-ttu-id="8851e-215">c.</span><span class="sxs-lookup"><span data-stu-id="8851e-215">c.</span></span> <span data-ttu-id="8851e-216">Select **Allow programmatic and AWS Management Console access**.</span><span class="sxs-lookup"><span data-stu-id="8851e-216">Select **Allow programmatic and AWS Management Console access**.</span></span>
  
    <span data-ttu-id="8851e-217">d.</span><span class="sxs-lookup"><span data-stu-id="8851e-217">d.</span></span> <span data-ttu-id="8851e-218">Click **Next: Permissions**.</span><span class="sxs-lookup"><span data-stu-id="8851e-218">Click **Next: Permissions**.</span></span>

16. <span data-ttu-id="8851e-219">On the **Attach Permissions Policies** dialog, click **Next: Review**.</span><span class="sxs-lookup"><span data-stu-id="8851e-219">On the **Attach Permissions Policies** dialog, click **Next: Review**.</span></span>  

    ![Configure Single Sign-On Policy][33]

17. <span data-ttu-id="8851e-221">On the **Review** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8851e-221">On the **Review** dialog, perform the following steps:</span></span>

    ![Configure Single Sign-On Review][34]

    <span data-ttu-id="8851e-223">a.</span><span class="sxs-lookup"><span data-stu-id="8851e-223">a.</span></span> <span data-ttu-id="8851e-224">In the **Role name** textbox, enter your Role name.</span><span class="sxs-lookup"><span data-stu-id="8851e-224">In the **Role name** textbox, enter your Role name.</span></span>

    <span data-ttu-id="8851e-225">b.</span><span class="sxs-lookup"><span data-stu-id="8851e-225">b.</span></span> <span data-ttu-id="8851e-226">In the **Role description** textbox, enter the description.</span><span class="sxs-lookup"><span data-stu-id="8851e-226">In the **Role description** textbox, enter the description.</span></span>

    <span data-ttu-id="8851e-227">a.</span><span class="sxs-lookup"><span data-stu-id="8851e-227">a.</span></span> <span data-ttu-id="8851e-228">Click **Create Role**.</span><span class="sxs-lookup"><span data-stu-id="8851e-228">Click **Create Role**.</span></span>

    <span data-ttu-id="8851e-229">b.</span><span class="sxs-lookup"><span data-stu-id="8851e-229">b.</span></span> <span data-ttu-id="8851e-230">Create as many roles as needed and map them to the Identity Provider.</span><span class="sxs-lookup"><span data-stu-id="8851e-230">Create as many roles as needed and map them to the Identity Provider.</span></span>

18. <span data-ttu-id="8851e-231">Sign out from current AWS account and login with other account where you want to configure single sign on with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8851e-231">Sign out from current AWS account and login with other account where you want to configure single sign on with Azure AD.</span></span>

19. <span data-ttu-id="8851e-232">Perform step-9 to step-17 to create multiple roles that you want to setup for this account.</span><span class="sxs-lookup"><span data-stu-id="8851e-232">Perform step-9 to step-17 to create multiple roles that you want to setup for this account.</span></span> <span data-ttu-id="8851e-233">If you have more than two accounts, please perform the same steps for all the accounts to create roles for them.</span><span class="sxs-lookup"><span data-stu-id="8851e-233">If you have more than two accounts, please perform the same steps for all the accounts to create roles for them.</span></span>

20. <span data-ttu-id="8851e-234">Once all the roles are created in the accounts, they show up in the **Roles** list for those accounts.</span><span class="sxs-lookup"><span data-stu-id="8851e-234">Once all the roles are created in the accounts, they show up in the **Roles** list for those accounts.</span></span>

    ![Roles setup](./media/aws-multi-accounts-tutorial/tutorial_amazonwebservices(aws)_listofroles.png)

21. <span data-ttu-id="8851e-236">We need to capture all the Role ARN and Trusted Entities for all the roles across all the accounts, which we need to map manually with Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="8851e-236">We need to capture all the Role ARN and Trusted Entities for all the roles across all the accounts, which we need to map manually with Azure AD application.</span></span> 

22. <span data-ttu-id="8851e-237">Click on the roles to copy **Role ARN** and **Trusted Entities** values.</span><span class="sxs-lookup"><span data-stu-id="8851e-237">Click on the roles to copy **Role ARN** and **Trusted Entities** values.</span></span> <span data-ttu-id="8851e-238">You need these values for all the roles that you need to create in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8851e-238">You need these values for all the roles that you need to create in Azure AD.</span></span>

    ![Roles setup](./media/aws-multi-accounts-tutorial/tutorial_amazonwebservices(aws)_role_summary.png)

23. <span data-ttu-id="8851e-240">Perform the above step for all the roles in all the accounts and store all of them in format **Role ARN,Trusted entities** in a notepad.</span><span class="sxs-lookup"><span data-stu-id="8851e-240">Perform the above step for all the roles in all the accounts and store all of them in format **Role ARN,Trusted entities** in a notepad.</span></span>

24. <span data-ttu-id="8851e-241">Open [Azure AD Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) in another window.</span><span class="sxs-lookup"><span data-stu-id="8851e-241">Open [Azure AD Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) in another window.</span></span>

    <span data-ttu-id="8851e-242">a.</span><span class="sxs-lookup"><span data-stu-id="8851e-242">a.</span></span> <span data-ttu-id="8851e-243">Sign in to the Graph Explorer site using the Global Admin/Co-admin credentials for your tenant.</span><span class="sxs-lookup"><span data-stu-id="8851e-243">Sign in to the Graph Explorer site using the Global Admin/Co-admin credentials for your tenant.</span></span>

    <span data-ttu-id="8851e-244">b.</span><span class="sxs-lookup"><span data-stu-id="8851e-244">b.</span></span> <span data-ttu-id="8851e-245">You need to have sufficient permissions to create the roles.</span><span class="sxs-lookup"><span data-stu-id="8851e-245">You need to have sufficient permissions to create the roles.</span></span> <span data-ttu-id="8851e-246">Click on **modify permissions** to get the required permissions.</span><span class="sxs-lookup"><span data-stu-id="8851e-246">Click on **modify permissions** to get the required permissions.</span></span>

    ![Graph explorer dialog box](./media/aws-multi-accounts-tutorial/graph-explorer-new9.png)

    <span data-ttu-id="8851e-248">c.</span><span class="sxs-lookup"><span data-stu-id="8851e-248">c.</span></span> <span data-ttu-id="8851e-249">Select following permissions from the list (if you don't have these already) and click "Modify Permissions"</span><span class="sxs-lookup"><span data-stu-id="8851e-249">Select following permissions from the list (if you don't have these already) and click "Modify Permissions"</span></span> 

    ![Graph explorer dialog box](./media/aws-multi-accounts-tutorial/graph-explorer-new10.png)

    <span data-ttu-id="8851e-251">d.</span><span class="sxs-lookup"><span data-stu-id="8851e-251">d.</span></span> <span data-ttu-id="8851e-252">This will ask you to login again and accept the consent.</span><span class="sxs-lookup"><span data-stu-id="8851e-252">This will ask you to login again and accept the consent.</span></span> <span data-ttu-id="8851e-253">After accepting the consent, you are logged into the Graph Explorer again.</span><span class="sxs-lookup"><span data-stu-id="8851e-253">After accepting the consent, you are logged into the Graph Explorer again.</span></span>

    <span data-ttu-id="8851e-254">e.</span><span class="sxs-lookup"><span data-stu-id="8851e-254">e.</span></span> <span data-ttu-id="8851e-255">Change the version dropdown to **beta**.</span><span class="sxs-lookup"><span data-stu-id="8851e-255">Change the version dropdown to **beta**.</span></span> <span data-ttu-id="8851e-256">To fetch all the Service Principals from your tenant, use the following query:</span><span class="sxs-lookup"><span data-stu-id="8851e-256">To fetch all the Service Principals from your tenant, use the following query:</span></span>

     `https://graph.microsoft.com/beta/servicePrincipals`

    <span data-ttu-id="8851e-257">If you are using multiple directories, then you can use following pattern, which has your primary domain in it `https://graph.microsoft.com/beta/contoso.com/servicePrincipals`</span><span class="sxs-lookup"><span data-stu-id="8851e-257">If you are using multiple directories, then you can use following pattern, which has your primary domain in it `https://graph.microsoft.com/beta/contoso.com/servicePrincipals`</span></span>

    ![Graph explorer dialog box](./media/aws-multi-accounts-tutorial/graph-explorer-new1.png)

    <span data-ttu-id="8851e-259">f.</span><span class="sxs-lookup"><span data-stu-id="8851e-259">f.</span></span> <span data-ttu-id="8851e-260">From the list of Service Principals fetched, get the one you need to modify.</span><span class="sxs-lookup"><span data-stu-id="8851e-260">From the list of Service Principals fetched, get the one you need to modify.</span></span> <span data-ttu-id="8851e-261">You can also use the Ctrl+F to search the application from all the listed ServicePrincipals.</span><span class="sxs-lookup"><span data-stu-id="8851e-261">You can also use the Ctrl+F to search the application from all the listed ServicePrincipals.</span></span> <span data-ttu-id="8851e-262">You can use following query by using the **Object id** which you have copied from Azure AD Properties page to get to the respective Service Principal.</span><span class="sxs-lookup"><span data-stu-id="8851e-262">You can use following query by using the **Object id** which you have copied from Azure AD Properties page to get to the respective Service Principal.</span></span>

    <span data-ttu-id="8851e-263">`https://graph.microsoft.com/beta/servicePrincipals/<objectID>`.</span><span class="sxs-lookup"><span data-stu-id="8851e-263">`https://graph.microsoft.com/beta/servicePrincipals/<objectID>`.</span></span>

    ![Graph explorer dialog box](./media/aws-multi-accounts-tutorial/graph-explorer-new2.png)

    <span data-ttu-id="8851e-265">g.</span><span class="sxs-lookup"><span data-stu-id="8851e-265">g.</span></span> <span data-ttu-id="8851e-266">Extract the appRoles property from the service principal object.</span><span class="sxs-lookup"><span data-stu-id="8851e-266">Extract the appRoles property from the service principal object.</span></span>

    ![Graph explorer dialog box](./media/aws-multi-accounts-tutorial/graph-explorer-new3.png)

    <span data-ttu-id="8851e-268">h.</span><span class="sxs-lookup"><span data-stu-id="8851e-268">h.</span></span> <span data-ttu-id="8851e-269">You now need to generate new roles for your application.</span><span class="sxs-lookup"><span data-stu-id="8851e-269">You now need to generate new roles for your application.</span></span> 

    <span data-ttu-id="8851e-270">i.</span><span class="sxs-lookup"><span data-stu-id="8851e-270">i.</span></span> <span data-ttu-id="8851e-271">Below JSON is an example of appRoles object.</span><span class="sxs-lookup"><span data-stu-id="8851e-271">Below JSON is an example of appRoles object.</span></span> <span data-ttu-id="8851e-272">Create a similar object to add the roles you want for your application.</span><span class="sxs-lookup"><span data-stu-id="8851e-272">Create a similar object to add the roles you want for your application.</span></span>

    ```
    {
    "appRoles": [
        {
            "allowedMemberTypes": [
                "User"
            ],
            "description": "msiam_access",
            "displayName": "msiam_access",
            "id": "7dfd756e-8c27-4472-b2b7-38c17fc5de5e",
            "isEnabled": true,
            "origin": "Application",
            "value": null
        },
        {
            "allowedMemberTypes": [
                "User"
            ],
            "description": "Admin,WAAD",
            "displayName": "Admin,WAAD",
            "id": "4aacf5a4-f38b-4861-b909-bae023e88dde",
            "isEnabled": true,
            "origin": "ServicePrincipal",
            "value": "arn:aws:iam::12345:role/Admin,arn:aws:iam::12345:saml-provider/WAAD"
        },
        {
            "allowedMemberTypes": [
                "User"
            ],
            "description": "Auditors,WAAD",
            "displayName": "Auditors,WAAD",
            "id": "bcad6926-67ec-445a-80f8-578032504c09",
            "isEnabled": true,
            "origin": "ServicePrincipal",
            "value": "arn:aws:iam::12345:role/Auditors,arn:aws:iam::12345:saml-provider/WAAD"
        }    ]
    }
    ```

    > [!Note]
    > <span data-ttu-id="8851e-273">You can only add new roles after the **msiam_access** for the patch operation.</span><span class="sxs-lookup"><span data-stu-id="8851e-273">You can only add new roles after the **msiam_access** for the patch operation.</span></span> <span data-ttu-id="8851e-274">Also, you can add as many roles as you want per your Organization need.</span><span class="sxs-lookup"><span data-stu-id="8851e-274">Also, you can add as many roles as you want per your Organization need.</span></span> <span data-ttu-id="8851e-275">Azure AD will send the **value** of these roles as the claim value in SAML response.</span><span class="sxs-lookup"><span data-stu-id="8851e-275">Azure AD will send the **value** of these roles as the claim value in SAML response.</span></span>

    <span data-ttu-id="8851e-276">j.</span><span class="sxs-lookup"><span data-stu-id="8851e-276">j.</span></span> <span data-ttu-id="8851e-277">Go back to your Graph Explorer and change the method from **GET** to **PATCH**.</span><span class="sxs-lookup"><span data-stu-id="8851e-277">Go back to your Graph Explorer and change the method from **GET** to **PATCH**.</span></span> <span data-ttu-id="8851e-278">Patch the Service Principal object to have desired roles by updating appRoles property similar to the one shown above in the example.</span><span class="sxs-lookup"><span data-stu-id="8851e-278">Patch the Service Principal object to have desired roles by updating appRoles property similar to the one shown above in the example.</span></span> <span data-ttu-id="8851e-279">Click **Run Query** to execute the patch operation.</span><span class="sxs-lookup"><span data-stu-id="8851e-279">Click **Run Query** to execute the patch operation.</span></span> <span data-ttu-id="8851e-280">A success message confirms the creation of the role for your Amazon Web Services application.</span><span class="sxs-lookup"><span data-stu-id="8851e-280">A success message confirms the creation of the role for your Amazon Web Services application.</span></span>

    ![Graph explorer dialog box](./media/aws-multi-accounts-tutorial/graph-explorer-new11.png)

25. <span data-ttu-id="8851e-282">After the Service Principal is patched with more roles, you can assign Users/Groups to the respective roles.</span><span class="sxs-lookup"><span data-stu-id="8851e-282">After the Service Principal is patched with more roles, you can assign Users/Groups to the respective roles.</span></span> <span data-ttu-id="8851e-283">This can be done by going to portal and navigating to the Amazon Web Services application.</span><span class="sxs-lookup"><span data-stu-id="8851e-283">This can be done by going to portal and navigating to the Amazon Web Services application.</span></span> <span data-ttu-id="8851e-284">Click on the **Users and Groups** tab on the top.</span><span class="sxs-lookup"><span data-stu-id="8851e-284">Click on the **Users and Groups** tab on the top.</span></span> 

26. <span data-ttu-id="8851e-285">We recommend you to create new groups for every AWS role so that you can assign that particular role in that group.</span><span class="sxs-lookup"><span data-stu-id="8851e-285">We recommend you to create new groups for every AWS role so that you can assign that particular role in that group.</span></span> <span data-ttu-id="8851e-286">Note that this is one to one mapping for one group to one role.</span><span class="sxs-lookup"><span data-stu-id="8851e-286">Note that this is one to one mapping for one group to one role.</span></span> <span data-ttu-id="8851e-287">You can then add the members who belong to that group.</span><span class="sxs-lookup"><span data-stu-id="8851e-287">You can then add the members who belong to that group.</span></span>

27. <span data-ttu-id="8851e-288">Once the Groups are created, select the group and assign to the application.</span><span class="sxs-lookup"><span data-stu-id="8851e-288">Once the Groups are created, select the group and assign to the application.</span></span>

    ![Configure Single Sign-On Add](./media/aws-multi-accounts-tutorial/graph-explorer-new5.png)

> [!Note]
> <span data-ttu-id="8851e-290">Nested groups are not supported when assigning groups.</span><span class="sxs-lookup"><span data-stu-id="8851e-290">Nested groups are not supported when assigning groups.</span></span>

28. <span data-ttu-id="8851e-291">To assign the role to the group, select the role and click on **Assign** button in the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="8851e-291">To assign the role to the group, select the role and click on **Assign** button in the bottom of the page.</span></span>

    ![Configure Single Sign-On Add](./media/aws-multi-accounts-tutorial/graph-explorer-new6.png)

> [!Note]
> <span data-ttu-id="8851e-293">Please note that you need to refresh your session in Azure portal to see new roles.</span><span class="sxs-lookup"><span data-stu-id="8851e-293">Please note that you need to refresh your session in Azure portal to see new roles.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="8851e-294">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="8851e-294">Test single sign-on</span></span>

<span data-ttu-id="8851e-295">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8851e-295">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8851e-296">When you click the Amazon Web Services (AWS) tile in the Access Panel, you should get Amazon Web Services (AWS) application page with option to select the role.</span><span class="sxs-lookup"><span data-stu-id="8851e-296">When you click the Amazon Web Services (AWS) tile in the Access Panel, you should get Amazon Web Services (AWS) application page with option to select the role.</span></span>

![Configure Single Sign-On Add](./media/aws-multi-accounts-tutorial/tutorial_amazonwebservices(aws)_test_screen.png)

<span data-ttu-id="8851e-298">You can also verify the SAML response to see the roles being passed as claims.</span><span class="sxs-lookup"><span data-stu-id="8851e-298">You can also verify the SAML response to see the roles being passed as claims.</span></span>

![Configure Single Sign-On Add](./media/aws-multi-accounts-tutorial/tutorial_amazonwebservices(aws)_test_saml.png)

<span data-ttu-id="8851e-300">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8851e-300">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8851e-301">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8851e-301">Additional resources</span></span>

* [<span data-ttu-id="8851e-302">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8851e-302">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="8851e-303">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8851e-303">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/aws-multi-accounts-tutorial/tutorial_general_01.png
[2]: ./media/aws-multi-accounts-tutorial/tutorial_general_02.png
[3]: ./media/aws-multi-accounts-tutorial/tutorial_general_03.png
[4]: ./media/aws-multi-accounts-tutorial/tutorial_general_04.png

[100]: ./media/aws-multi-accounts-tutorial/tutorial_general_100.png

[200]: ./media/aws-multi-accounts-tutorial/tutorial_general_200.png
[201]: ./media/aws-multi-accounts-tutorial/tutorial_general_201.png
[202]: ./media/aws-multi-accounts-tutorial/tutorial_general_202.png
[203]: ./media/aws-multi-accounts-tutorial/tutorial_general_203.png
[11]: ./media/aws-multi-accounts-tutorial/ic795031.png
[12]: ./media/aws-multi-accounts-tutorial/ic795032.png
[13]: ./media/aws-multi-accounts-tutorial/ic795033.png
[14]: ./media/aws-multi-accounts-tutorial/ic795034.png
[15]: ./media/aws-multi-accounts-tutorial/ic795035.png
[16]: ./media/aws-multi-accounts-tutorial/ic795022.png
[17]: ./media/aws-multi-accounts-tutorial/ic795023.png
[18]: ./media/aws-multi-accounts-tutorial/ic795024.png
[19]: ./media/aws-multi-accounts-tutorial/ic795025.png
[32]: ./media/aws-multi-accounts-tutorial/ic7950251.png
[33]: ./media/aws-multi-accounts-tutorial/ic7950252.png
[35]: ./media/aws-multi-accounts-tutorial/tutorial_amazonwebservices_provisioning.png
[34]: ./media/aws-multi-accounts-tutorial/ic7950253.png
[36]: ./media/aws-multi-accounts-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/aws-multi-accounts-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/aws-multi-accounts-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/aws-multi-accounts-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/aws-multi-accounts-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/aws-multi-accounts-tutorial/tutorial_amazonwebservices_provisioning_on.png

