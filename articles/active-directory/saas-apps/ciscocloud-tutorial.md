---
title: 'Tutorial: Azure Active Directory integration with Cisco Cloud | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Cisco Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: db1cea1d-ff0a-4f0d-b5fd-50ca32702d56
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2018
ms.author: jeedes
ms.openlocfilehash: e5d7e195a3f61d32387d1101fbb24bfa1ac8bccb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858133"
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-cloud"></a><span data-ttu-id="71894-103">Tutorial: Azure Active Directory integration with Cisco Cloud</span><span class="sxs-lookup"><span data-stu-id="71894-103">Tutorial: Azure Active Directory integration with Cisco Cloud</span></span>

<span data-ttu-id="71894-104">In this tutorial, you learn how to integrate Cisco Cloud with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="71894-104">In this tutorial, you learn how to integrate Cisco Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="71894-105">Integrating Cisco Cloud with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="71894-105">Integrating Cisco Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="71894-106">You can control in Azure AD who has access to Cisco Cloud.</span><span class="sxs-lookup"><span data-stu-id="71894-106">You can control in Azure AD who has access to Cisco Cloud.</span></span>
- <span data-ttu-id="71894-107">You can enable your users to automatically get signed-on to Cisco Cloud (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="71894-107">You can enable your users to automatically get signed-on to Cisco Cloud (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="71894-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="71894-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="71894-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="71894-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71894-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="71894-110">Prerequisites</span></span>

<span data-ttu-id="71894-111">To configure Azure AD integration with Cisco Cloud, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="71894-111">To configure Azure AD integration with Cisco Cloud, you need the following items:</span></span>

- <span data-ttu-id="71894-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="71894-112">An Azure AD subscription</span></span>
- <span data-ttu-id="71894-113">A Cisco Cloud single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="71894-113">A Cisco Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="71894-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="71894-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="71894-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="71894-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="71894-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="71894-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="71894-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="71894-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="71894-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="71894-118">Scenario description</span></span>
<span data-ttu-id="71894-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="71894-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="71894-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="71894-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="71894-121">Adding Cisco Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="71894-121">Adding Cisco Cloud from the gallery</span></span>
1. <span data-ttu-id="71894-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="71894-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-cloud-from-the-gallery"></a><span data-ttu-id="71894-123">Adding Cisco Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="71894-123">Adding Cisco Cloud from the gallery</span></span>
<span data-ttu-id="71894-124">To configure the integration of Cisco Cloud into Azure AD, you need to add Cisco Cloud from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="71894-124">To configure the integration of Cisco Cloud into Azure AD, you need to add Cisco Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="71894-125">**To add Cisco Cloud from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="71894-125">**To add Cisco Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="71894-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="71894-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="71894-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="71894-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="71894-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="71894-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="71894-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="71894-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="71894-133">In the search box, type **Cisco Cloud**, select **Cisco Cloud** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="71894-133">In the search box, type **Cisco Cloud**, select **Cisco Cloud** from result panel then click **Add** button to add the application.</span></span>

    ![Cisco Cloud in the results list](./media/ciscocloud-tutorial/tutorial_ciscocloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="71894-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="71894-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="71894-136">In this section, you configure and test Azure AD single sign-on with Cisco Cloud based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="71894-136">In this section, you configure and test Azure AD single sign-on with Cisco Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="71894-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Cisco Cloud is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71894-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Cisco Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="71894-138">In other words, a link relationship between an Azure AD user and the related user in Cisco Cloud needs to be established.</span><span class="sxs-lookup"><span data-stu-id="71894-138">In other words, a link relationship between an Azure AD user and the related user in Cisco Cloud needs to be established.</span></span>

<span data-ttu-id="71894-139">To configure and test Azure AD single sign-on with Cisco Cloud, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="71894-139">To configure and test Azure AD single sign-on with Cisco Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="71894-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="71894-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="71894-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="71894-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="71894-142">**[Create a Cisco Cloud test user](#create-a-cisco-cloud-test-user)** - to have a counterpart of Britta Simon in Cisco Cloud that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="71894-142">**[Create a Cisco Cloud test user](#create-a-cisco-cloud-test-user)** - to have a counterpart of Britta Simon in Cisco Cloud that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="71894-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="71894-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="71894-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="71894-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="71894-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="71894-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="71894-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cisco Cloud application.</span><span class="sxs-lookup"><span data-stu-id="71894-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cisco Cloud application.</span></span>

<span data-ttu-id="71894-147">**To configure Azure AD single sign-on with Cisco Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="71894-147">**To configure Azure AD single sign-on with Cisco Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="71894-148">In the Azure portal, on the **Cisco Cloud** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="71894-148">In the Azure portal, on the **Cisco Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="71894-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="71894-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/ciscocloud-tutorial/tutorial_ciscocloud_samlbase.png)

1. <span data-ttu-id="71894-152">On the **Cisco Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="71894-152">On the **Cisco Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Cisco Cloud Domain and URLs single sign-on information](./media/ciscocloud-tutorial/tutorial_ciscocloud_url.png)

    <span data-ttu-id="71894-154">a.</span><span class="sxs-lookup"><span data-stu-id="71894-154">a.</span></span> <span data-ttu-id="71894-155">In the **Identifier** textbox, type a URL using the following pattern: `<subdomain>.cisco.com`</span><span class="sxs-lookup"><span data-stu-id="71894-155">In the **Identifier** textbox, type a URL using the following pattern: `<subdomain>.cisco.com`</span></span>

    <span data-ttu-id="71894-156">b.</span><span class="sxs-lookup"><span data-stu-id="71894-156">b.</span></span> <span data-ttu-id="71894-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.cisco.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="71894-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.cisco.com/sp/ACS.saml2`</span></span>

1. <span data-ttu-id="71894-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="71894-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Cisco Cloud Domain and URLs single sign-on information](./media/ciscocloud-tutorial/tutorial_ciscocloud_url1.png)

    <span data-ttu-id="71894-160">In the **Sign-on URL** textbox, type a URL: `https://<subdomain>.cloudapps.cisco.com`</span><span class="sxs-lookup"><span data-stu-id="71894-160">In the **Sign-on URL** textbox, type a URL: `https://<subdomain>.cloudapps.cisco.com`</span></span>

    > [!NOTE]
    > <span data-ttu-id="71894-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="71894-161">These values are not real.</span></span> <span data-ttu-id="71894-162">Update these values with the actual Identifier, Reply URL and Sign on URL.</span><span class="sxs-lookup"><span data-stu-id="71894-162">Update these values with the actual Identifier, Reply URL and Sign on URL.</span></span> <span data-ttu-id="71894-163">Contact [Cisco Cloud Client support team](mailto:cpr-ops@cisco.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="71894-163">Contact [Cisco Cloud Client support team](mailto:cpr-ops@cisco.com) to get these values.</span></span>

1. <span data-ttu-id="71894-164">Cisco Cloud application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="71894-164">Cisco Cloud application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="71894-165">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="71894-165">Configure the following claims for this application.</span></span> <span data-ttu-id="71894-166">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="71894-166">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="71894-167">The following screenshot shows an example about it.</span><span class="sxs-lookup"><span data-stu-id="71894-167">The following screenshot shows an example about it.</span></span>

    ![Configure Single Sign-On](./media/ciscocloud-tutorial/attribute.png)

1. <span data-ttu-id="71894-169">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span><span class="sxs-lookup"><span data-stu-id="71894-169">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="71894-170">Perform the following steps on each of the displayed attributes-</span><span class="sxs-lookup"><span data-stu-id="71894-170">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="71894-171">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="71894-171">Attribute Name</span></span> | <span data-ttu-id="71894-172">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="71894-172">Attribute Value</span></span> |
    | ---------------| ----------------|
    | <span data-ttu-id="71894-173">country</span><span class="sxs-lookup"><span data-stu-id="71894-173">country</span></span>      |<span data-ttu-id="71894-174">user.country</span><span class="sxs-lookup"><span data-stu-id="71894-174">user.country</span></span> |
    | <span data-ttu-id="71894-175">company</span><span class="sxs-lookup"><span data-stu-id="71894-175">company</span></span>      |<span data-ttu-id="71894-176">user.companyname</span><span class="sxs-lookup"><span data-stu-id="71894-176">user.companyname</span></span> |

    <span data-ttu-id="71894-177">a.</span><span class="sxs-lookup"><span data-stu-id="71894-177">a.</span></span> <span data-ttu-id="71894-178">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="71894-178">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/ciscocloud-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/ciscocloud-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="71894-181">b.</span><span class="sxs-lookup"><span data-stu-id="71894-181">b.</span></span> <span data-ttu-id="71894-182">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="71894-182">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="71894-183">c.</span><span class="sxs-lookup"><span data-stu-id="71894-183">c.</span></span> <span data-ttu-id="71894-184">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="71894-184">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="71894-185">d.</span><span class="sxs-lookup"><span data-stu-id="71894-185">d.</span></span> <span data-ttu-id="71894-186">Leave **Namespace** value as blank.</span><span class="sxs-lookup"><span data-stu-id="71894-186">Leave **Namespace** value as blank.</span></span>

    <span data-ttu-id="71894-187">e.</span><span class="sxs-lookup"><span data-stu-id="71894-187">e.</span></span> <span data-ttu-id="71894-188">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="71894-188">Click **Ok**.</span></span>

1. <span data-ttu-id="71894-189">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="71894-189">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

    ![The Certificate download link](./media/ciscocloud-tutorial/tutorial_ciscocloud_certificate.png)

1. <span data-ttu-id="71894-191">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="71894-191">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/ciscocloud-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="71894-193">To configure single sign-on on **Cisco Cloud** side, you need to send the **App Federation Metadata Url** to [Cisco Cloud support team](mailto:cpr-ops@cisco.com).</span><span class="sxs-lookup"><span data-stu-id="71894-193">To configure single sign-on on **Cisco Cloud** side, you need to send the **App Federation Metadata Url** to [Cisco Cloud support team](mailto:cpr-ops@cisco.com).</span></span> <span data-ttu-id="71894-194">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="71894-194">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="71894-195">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="71894-195">Create an Azure AD test user</span></span>

<span data-ttu-id="71894-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="71894-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="71894-198">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="71894-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="71894-199">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="71894-199">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/ciscocloud-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="71894-201">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="71894-201">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/ciscocloud-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="71894-203">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="71894-203">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/ciscocloud-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="71894-205">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="71894-205">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/ciscocloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="71894-207">a.</span><span class="sxs-lookup"><span data-stu-id="71894-207">a.</span></span> <span data-ttu-id="71894-208">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="71894-208">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="71894-209">b.</span><span class="sxs-lookup"><span data-stu-id="71894-209">b.</span></span> <span data-ttu-id="71894-210">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="71894-210">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="71894-211">c.</span><span class="sxs-lookup"><span data-stu-id="71894-211">c.</span></span> <span data-ttu-id="71894-212">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="71894-212">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="71894-213">d.</span><span class="sxs-lookup"><span data-stu-id="71894-213">d.</span></span> <span data-ttu-id="71894-214">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="71894-214">Click **Create**.</span></span>
 
### <a name="create-a-cisco-cloud-test-user"></a><span data-ttu-id="71894-215">Create a Cisco Cloud test user</span><span class="sxs-lookup"><span data-stu-id="71894-215">Create a Cisco Cloud test user</span></span>

<span data-ttu-id="71894-216">In this section, you create a user called Britta Simon in Cisco Cloud.</span><span class="sxs-lookup"><span data-stu-id="71894-216">In this section, you create a user called Britta Simon in Cisco Cloud.</span></span> <span data-ttu-id="71894-217">Work with [Cisco Cloud support team](mailto:cpr-ops@cisco.com) to add the users in the Cisco Cloud platform.</span><span class="sxs-lookup"><span data-stu-id="71894-217">Work with [Cisco Cloud support team](mailto:cpr-ops@cisco.com) to add the users in the Cisco Cloud platform.</span></span> <span data-ttu-id="71894-218">Users must be created and activated before you use single sign-on</span><span class="sxs-lookup"><span data-stu-id="71894-218">Users must be created and activated before you use single sign-on</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="71894-219">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="71894-219">Assign the Azure AD test user</span></span>

<span data-ttu-id="71894-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cisco Cloud.</span><span class="sxs-lookup"><span data-stu-id="71894-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cisco Cloud.</span></span>

![Assign the user role][200] 

<span data-ttu-id="71894-222">**To assign Britta Simon to Cisco Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="71894-222">**To assign Britta Simon to Cisco Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="71894-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="71894-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="71894-225">In the applications list, select **Cisco Cloud**.</span><span class="sxs-lookup"><span data-stu-id="71894-225">In the applications list, select **Cisco Cloud**.</span></span>

    ![The Cisco Cloud link in the Applications list](./media/ciscocloud-tutorial/tutorial_ciscocloud_app.png)  

1. <span data-ttu-id="71894-227">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="71894-227">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="71894-229">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="71894-229">Click **Add** button.</span></span> <span data-ttu-id="71894-230">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="71894-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="71894-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="71894-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="71894-233">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="71894-233">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="71894-234">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="71894-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="71894-235">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="71894-235">Test single sign-on</span></span>

<span data-ttu-id="71894-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="71894-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="71894-237">When you click the Cisco Cloud tile in the Access Panel, you should get automatically signed-on to your Cisco Cloud application.</span><span class="sxs-lookup"><span data-stu-id="71894-237">When you click the Cisco Cloud tile in the Access Panel, you should get automatically signed-on to your Cisco Cloud application.</span></span>
<span data-ttu-id="71894-238">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="71894-238">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="71894-239">Additional resources</span><span class="sxs-lookup"><span data-stu-id="71894-239">Additional resources</span></span>

* [<span data-ttu-id="71894-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="71894-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="71894-241">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="71894-241">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/ciscocloud-tutorial/tutorial_general_01.png
[2]: ./media/ciscocloud-tutorial/tutorial_general_02.png
[3]: ./media/ciscocloud-tutorial/tutorial_general_03.png
[4]: ./media/ciscocloud-tutorial/tutorial_general_04.png

[100]: ./media/ciscocloud-tutorial/tutorial_general_100.png

[200]: ./media/ciscocloud-tutorial/tutorial_general_200.png
[201]: ./media/ciscocloud-tutorial/tutorial_general_201.png
[202]: ./media/ciscocloud-tutorial/tutorial_general_202.png
[203]: ./media/ciscocloud-tutorial/tutorial_general_203.png

