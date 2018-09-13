---
title: 'Tutorial: Azure Active Directory integration with Trisotech Digital Enterprise Server | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Trisotech Digital Enterprise Server.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6d54d20c-eca1-4fa6-b56a-4c3ed0593db0
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/16/2018
ms.author: jeedes
ms.openlocfilehash: e36a4be3a95b67c040855171d4b167e495a22496
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865689"
---
# <a name="tutorial-azure-active-directory-integration-with-trisotech-digital-enterprise-server"></a><span data-ttu-id="b27c9-103">Tutorial: Azure Active Directory integration with Trisotech Digital Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="b27c9-103">Tutorial: Azure Active Directory integration with Trisotech Digital Enterprise Server</span></span>

<span data-ttu-id="b27c9-104">In this tutorial, you learn how to integrate Trisotech Digital Enterprise Server with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b27c9-104">In this tutorial, you learn how to integrate Trisotech Digital Enterprise Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b27c9-105">Integrating Trisotech Digital Enterprise Server with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="b27c9-105">Integrating Trisotech Digital Enterprise Server with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b27c9-106">You can control in Azure AD who has access to Trisotech Digital Enterprise Server.</span><span class="sxs-lookup"><span data-stu-id="b27c9-106">You can control in Azure AD who has access to Trisotech Digital Enterprise Server.</span></span>
- <span data-ttu-id="b27c9-107">You can enable your users to automatically get signed-on to Trisotech Digital Enterprise Server (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="b27c9-107">You can enable your users to automatically get signed-on to Trisotech Digital Enterprise Server (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b27c9-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b27c9-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b27c9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="b27c9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b27c9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b27c9-110">Prerequisites</span></span>

<span data-ttu-id="b27c9-111">To configure Azure AD integration with Trisotech Digital Enterprise Server, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="b27c9-111">To configure Azure AD integration with Trisotech Digital Enterprise Server, you need the following items:</span></span>

- <span data-ttu-id="b27c9-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="b27c9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b27c9-113">A Trisotech Digital Enterprise Server single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b27c9-113">A Trisotech Digital Enterprise Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b27c9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="b27c9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b27c9-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="b27c9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b27c9-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="b27c9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b27c9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b27c9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b27c9-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="b27c9-118">Scenario description</span></span>
<span data-ttu-id="b27c9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="b27c9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b27c9-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="b27c9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b27c9-121">Adding Trisotech Digital Enterprise Server from the gallery</span><span class="sxs-lookup"><span data-stu-id="b27c9-121">Adding Trisotech Digital Enterprise Server from the gallery</span></span>
1. <span data-ttu-id="b27c9-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b27c9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trisotech-digital-enterprise-server-from-the-gallery"></a><span data-ttu-id="b27c9-123">Adding Trisotech Digital Enterprise Server from the gallery</span><span class="sxs-lookup"><span data-stu-id="b27c9-123">Adding Trisotech Digital Enterprise Server from the gallery</span></span>
<span data-ttu-id="b27c9-124">To configure the integration of Trisotech Digital Enterprise Server into Azure AD, you need to add Trisotech Digital Enterprise Server from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="b27c9-124">To configure the integration of Trisotech Digital Enterprise Server into Azure AD, you need to add Trisotech Digital Enterprise Server from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b27c9-125">**To add Trisotech Digital Enterprise Server from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b27c9-125">**To add Trisotech Digital Enterprise Server from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b27c9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="b27c9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="b27c9-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="b27c9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b27c9-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b27c9-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="b27c9-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="b27c9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="b27c9-133">In the search box, type **Trisotech Digital Enterprise Server**, select **Trisotech Digital Enterprise Server** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="b27c9-133">In the search box, type **Trisotech Digital Enterprise Server**, select **Trisotech Digital Enterprise Server** from result panel then click **Add** button to add the application.</span></span>

    ![Trisotech Digital Enterprise Server in the results list](./media/trisotechdigitalenterpriseserver-tutorial/tutorial_trisotechdigitalenterpriseserver_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b27c9-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b27c9-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b27c9-136">In this section, you configure and test Azure AD single sign-on with Trisotech Digital Enterprise Server based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b27c9-136">In this section, you configure and test Azure AD single sign-on with Trisotech Digital Enterprise Server based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b27c9-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Trisotech Digital Enterprise Server is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b27c9-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Trisotech Digital Enterprise Server is to a user in Azure AD.</span></span> <span data-ttu-id="b27c9-138">In other words, a link relationship between an Azure AD user and the related user in Trisotech Digital Enterprise Server needs to be established.</span><span class="sxs-lookup"><span data-stu-id="b27c9-138">In other words, a link relationship between an Azure AD user and the related user in Trisotech Digital Enterprise Server needs to be established.</span></span>

<span data-ttu-id="b27c9-139">To configure and test Azure AD single sign-on with Trisotech Digital Enterprise Server, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b27c9-139">To configure and test Azure AD single sign-on with Trisotech Digital Enterprise Server, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b27c9-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="b27c9-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="b27c9-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b27c9-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="b27c9-142">**[Create a Trisotech Digital Enterprise Server test user](#create-a-trisotech-digital-enterprise-server-test-user)** - to have a counterpart of Britta Simon in Trisotech Digital Enterprise Server that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="b27c9-142">**[Create a Trisotech Digital Enterprise Server test user](#create-a-trisotech-digital-enterprise-server-test-user)** - to have a counterpart of Britta Simon in Trisotech Digital Enterprise Server that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="b27c9-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b27c9-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="b27c9-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="b27c9-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b27c9-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b27c9-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b27c9-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trisotech Digital Enterprise Server application.</span><span class="sxs-lookup"><span data-stu-id="b27c9-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trisotech Digital Enterprise Server application.</span></span>

<span data-ttu-id="b27c9-147">**To configure Azure AD single sign-on with Trisotech Digital Enterprise Server, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b27c9-147">**To configure Azure AD single sign-on with Trisotech Digital Enterprise Server, perform the following steps:**</span></span>

1. <span data-ttu-id="b27c9-148">In the Azure portal, on the **Trisotech Digital Enterprise Server** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b27c9-148">In the Azure portal, on the **Trisotech Digital Enterprise Server** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="b27c9-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b27c9-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/trisotechdigitalenterpriseserver-tutorial/tutorial_trisotechdigitalenterpriseserver_samlbase.png)

1. <span data-ttu-id="b27c9-152">On the **Trisotech Digital Enterprise Server Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b27c9-152">On the **Trisotech Digital Enterprise Server Domain and URLs** section, perform the following steps:</span></span>

    ![Trisotech Digital Enterprise Server Domain and URLs single sign-on information](./media/trisotechdigitalenterpriseserver-tutorial/tutorial_trisotechdigitalenterpriseserver_url.png)

    <span data-ttu-id="b27c9-154">a.</span><span class="sxs-lookup"><span data-stu-id="b27c9-154">a.</span></span> <span data-ttu-id="b27c9-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.trisotech.com`</span><span class="sxs-lookup"><span data-stu-id="b27c9-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.trisotech.com`</span></span>

    <span data-ttu-id="b27c9-156">b.</span><span class="sxs-lookup"><span data-stu-id="b27c9-156">b.</span></span> <span data-ttu-id="b27c9-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.trisotech.com`</span><span class="sxs-lookup"><span data-stu-id="b27c9-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.trisotech.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b27c9-158">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="b27c9-158">These values are not real.</span></span> <span data-ttu-id="b27c9-159">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="b27c9-159">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b27c9-160">Contact [Trisotech Digital Enterprise Server Client support team](mailto:support@trisotech.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="b27c9-160">Contact [Trisotech Digital Enterprise Server Client support team](mailto:support@trisotech.com) to get these values.</span></span>

1. <span data-ttu-id="b27c9-161">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="b27c9-161">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span> 

    ![The Certificate download link](./media/trisotechdigitalenterpriseserver-tutorial/tutorial_trisotechdigitalenterpriseserver_certificate.png)

1. <span data-ttu-id="b27c9-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="b27c9-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/trisotechdigitalenterpriseserver-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="b27c9-165">In a different web browser window, log in to your Trisotech Digital Enterprise Server Configuration company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="b27c9-165">In a different web browser window, log in to your Trisotech Digital Enterprise Server Configuration company site as an administrator.</span></span>

1. <span data-ttu-id="b27c9-166">Click on the **Menu icon** and then select **Administration**.</span><span class="sxs-lookup"><span data-stu-id="b27c9-166">Click on the **Menu icon** and then select **Administration**.</span></span>

    ![Configure Single Sign-On](./media/trisotechdigitalenterpriseserver-tutorial/user1.png)

1. <span data-ttu-id="b27c9-168">Select **User Provider**.</span><span class="sxs-lookup"><span data-stu-id="b27c9-168">Select **User Provider**.</span></span>

    ![Configure Single Sign-On](./media/trisotechdigitalenterpriseserver-tutorial/user2.png)

1. <span data-ttu-id="b27c9-170">In the **User Provider Configurations** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b27c9-170">In the **User Provider Configurations** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/trisotechdigitalenterpriseserver-tutorial/user3.png)

    <span data-ttu-id="b27c9-172">a.</span><span class="sxs-lookup"><span data-stu-id="b27c9-172">a.</span></span> <span data-ttu-id="b27c9-173">Select **Secured Assertion Markup Language 2 (SAML 2)** from the dropdown in the **Authentication Method**.</span><span class="sxs-lookup"><span data-stu-id="b27c9-173">Select **Secured Assertion Markup Language 2 (SAML 2)** from the dropdown in the **Authentication Method**.</span></span>

    <span data-ttu-id="b27c9-174">b.</span><span class="sxs-lookup"><span data-stu-id="b27c9-174">b.</span></span> <span data-ttu-id="b27c9-175">In the **Metadata URL** textbox, paste the **App Federation Metadata Url** value, which you have copied form the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b27c9-175">In the **Metadata URL** textbox, paste the **App Federation Metadata Url** value, which you have copied form the Azure portal.</span></span>

    <span data-ttu-id="b27c9-176">c.</span><span class="sxs-lookup"><span data-stu-id="b27c9-176">c.</span></span> <span data-ttu-id="b27c9-177">In the **Application ID** textbox, enter the URL using the following pattern: `https://<companyname>.trisotech.com`.</span><span class="sxs-lookup"><span data-stu-id="b27c9-177">In the **Application ID** textbox, enter the URL using the following pattern: `https://<companyname>.trisotech.com`.</span></span>

    <span data-ttu-id="b27c9-178">d.</span><span class="sxs-lookup"><span data-stu-id="b27c9-178">d.</span></span> <span data-ttu-id="b27c9-179">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="b27c9-179">Click **Save**</span></span>

    <span data-ttu-id="b27c9-180">e.</span><span class="sxs-lookup"><span data-stu-id="b27c9-180">e.</span></span> <span data-ttu-id="b27c9-181">Enter the domain name in the **Allowed Domains (empty means everyone)** textbox, it automatically assigns licenses for users matching the Allowed Domains</span><span class="sxs-lookup"><span data-stu-id="b27c9-181">Enter the domain name in the **Allowed Domains (empty means everyone)** textbox, it automatically assigns licenses for users matching the Allowed Domains</span></span>

    <span data-ttu-id="b27c9-182">f.</span><span class="sxs-lookup"><span data-stu-id="b27c9-182">f.</span></span> <span data-ttu-id="b27c9-183">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="b27c9-183">Click **Save**</span></span>

 ### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b27c9-184">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b27c9-184">Create an Azure AD test user</span></span>

<span data-ttu-id="b27c9-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b27c9-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="b27c9-187">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b27c9-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b27c9-188">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="b27c9-188">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/trisotechdigitalenterpriseserver-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="b27c9-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="b27c9-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/trisotechdigitalenterpriseserver-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="b27c9-192">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="b27c9-192">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/trisotechdigitalenterpriseserver-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="b27c9-194">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b27c9-194">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/trisotechdigitalenterpriseserver-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b27c9-196">a.</span><span class="sxs-lookup"><span data-stu-id="b27c9-196">a.</span></span> <span data-ttu-id="b27c9-197">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b27c9-197">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b27c9-198">b.</span><span class="sxs-lookup"><span data-stu-id="b27c9-198">b.</span></span> <span data-ttu-id="b27c9-199">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b27c9-199">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b27c9-200">c.</span><span class="sxs-lookup"><span data-stu-id="b27c9-200">c.</span></span> <span data-ttu-id="b27c9-201">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="b27c9-201">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b27c9-202">d.</span><span class="sxs-lookup"><span data-stu-id="b27c9-202">d.</span></span> <span data-ttu-id="b27c9-203">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b27c9-203">Click **Create**.</span></span>
 
### <a name="create-a-trisotech-digital-enterprise-server-test-user"></a><span data-ttu-id="b27c9-204">Create a Trisotech Digital Enterprise Server test user</span><span class="sxs-lookup"><span data-stu-id="b27c9-204">Create a Trisotech Digital Enterprise Server test user</span></span>

<span data-ttu-id="b27c9-205">The objective of this section is to create a user called Britta Simon in Trisotech Digital Enterprise Server.</span><span class="sxs-lookup"><span data-stu-id="b27c9-205">The objective of this section is to create a user called Britta Simon in Trisotech Digital Enterprise Server.</span></span> <span data-ttu-id="b27c9-206">Trisotech Digital Enterprise Server supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="b27c9-206">Trisotech Digital Enterprise Server supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="b27c9-207">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="b27c9-207">There is no action item for you in this section.</span></span> <span data-ttu-id="b27c9-208">A new user is created during an attempt to access Trisotech Digital Enterprise Server if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="b27c9-208">A new user is created during an attempt to access Trisotech Digital Enterprise Server if it doesn't exist yet.</span></span>
>[!Note]
><span data-ttu-id="b27c9-209">If you need to create a user manually, contact [Trisotech Digital Enterprise Server support team](mailto:support@trisotech.com).</span><span class="sxs-lookup"><span data-stu-id="b27c9-209">If you need to create a user manually, contact [Trisotech Digital Enterprise Server support team](mailto:support@trisotech.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b27c9-210">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b27c9-210">Assign the Azure AD test user</span></span>

<span data-ttu-id="b27c9-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trisotech Digital Enterprise Server.</span><span class="sxs-lookup"><span data-stu-id="b27c9-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trisotech Digital Enterprise Server.</span></span>

![Assign the user role][200] 

<span data-ttu-id="b27c9-213">**To assign Britta Simon to Trisotech Digital Enterprise Server, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b27c9-213">**To assign Britta Simon to Trisotech Digital Enterprise Server, perform the following steps:**</span></span>

1. <span data-ttu-id="b27c9-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b27c9-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="b27c9-216">In the applications list, select **Trisotech Digital Enterprise Server**.</span><span class="sxs-lookup"><span data-stu-id="b27c9-216">In the applications list, select **Trisotech Digital Enterprise Server**.</span></span>

    ![The Trisotech Digital Enterprise Server link in the Applications list](./media/trisotechdigitalenterpriseserver-tutorial/tutorial_trisotechdigitalenterpriseserver_app.png)  

1. <span data-ttu-id="b27c9-218">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="b27c9-218">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="b27c9-220">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="b27c9-220">Click **Add** button.</span></span> <span data-ttu-id="b27c9-221">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b27c9-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="b27c9-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="b27c9-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="b27c9-224">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="b27c9-224">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="b27c9-225">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b27c9-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b27c9-226">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="b27c9-226">Test single sign-on</span></span>

<span data-ttu-id="b27c9-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b27c9-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b27c9-228">When you click the Trisotech Digital Enterprise Server tile in the Access Panel, you should get automatically signed-on to your Trisotech Digital Enterprise Server application.</span><span class="sxs-lookup"><span data-stu-id="b27c9-228">When you click the Trisotech Digital Enterprise Server tile in the Access Panel, you should get automatically signed-on to your Trisotech Digital Enterprise Server application.</span></span>
<span data-ttu-id="b27c9-229">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b27c9-229">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b27c9-230">Additional resources</span><span class="sxs-lookup"><span data-stu-id="b27c9-230">Additional resources</span></span>

* [<span data-ttu-id="b27c9-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b27c9-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="b27c9-232">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b27c9-232">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/trisotechdigitalenterpriseserver-tutorial/tutorial_general_01.png
[2]: ./media/trisotechdigitalenterpriseserver-tutorial/tutorial_general_02.png
[3]: ./media/trisotechdigitalenterpriseserver-tutorial/tutorial_general_03.png
[4]: ./media/trisotechdigitalenterpriseserver-tutorial/tutorial_general_04.png

[100]: ./media/trisotechdigitalenterpriseserver-tutorial/tutorial_general_100.png

[200]: ./media/trisotechdigitalenterpriseserver-tutorial/tutorial_general_200.png
[201]: ./media/trisotechdigitalenterpriseserver-tutorial/tutorial_general_201.png
[202]: ./media/trisotechdigitalenterpriseserver-tutorial/tutorial_general_202.png
[203]: ./media/trisotechdigitalenterpriseserver-tutorial/tutorial_general_203.png

