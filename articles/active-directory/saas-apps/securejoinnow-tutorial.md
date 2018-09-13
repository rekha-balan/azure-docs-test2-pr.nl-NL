---
title: 'Tutorial: Azure Active Directory integration with SecureW2 JoinNow Connector | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SecureW2 JoinNow Connector.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2445b3af-f827-40de-9097-6f5c933d0f53
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2018
ms.author: jeedes
ms.openlocfilehash: 283f8c935556006a21812578d0638b72adb6eed0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857622"
---
# <a name="tutorial-azure-active-directory-integration-with-securew2-joinnow-connector"></a><span data-ttu-id="f2f54-103">Tutorial: Azure Active Directory integration with SecureW2 JoinNow Connector</span><span class="sxs-lookup"><span data-stu-id="f2f54-103">Tutorial: Azure Active Directory integration with SecureW2 JoinNow Connector</span></span>

<span data-ttu-id="f2f54-104">In this tutorial, you learn how to integrate SecureW2 JoinNow Connector with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f2f54-104">In this tutorial, you learn how to integrate SecureW2 JoinNow Connector with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f2f54-105">Integrating SecureW2 JoinNow Connector with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f2f54-105">Integrating SecureW2 JoinNow Connector with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f2f54-106">You can control in Azure AD who has access to SecureW2 JoinNow Connector.</span><span class="sxs-lookup"><span data-stu-id="f2f54-106">You can control in Azure AD who has access to SecureW2 JoinNow Connector.</span></span>
- <span data-ttu-id="f2f54-107">You can enable your users to automatically get signed-on to SecureW2 JoinNow Connector (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="f2f54-107">You can enable your users to automatically get signed-on to SecureW2 JoinNow Connector (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f2f54-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f2f54-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f2f54-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="f2f54-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2f54-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f2f54-110">Prerequisites</span></span>

<span data-ttu-id="f2f54-111">To configure Azure AD integration with SecureW2 JoinNow Connector, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f2f54-111">To configure Azure AD integration with SecureW2 JoinNow Connector, you need the following items:</span></span>

- <span data-ttu-id="f2f54-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f2f54-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f2f54-113">A SecureW2 JoinNow Connector single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f2f54-113">A SecureW2 JoinNow Connector single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f2f54-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f2f54-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f2f54-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f2f54-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f2f54-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="f2f54-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f2f54-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f2f54-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f2f54-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f2f54-118">Scenario description</span></span>
<span data-ttu-id="f2f54-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f2f54-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f2f54-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f2f54-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f2f54-121">Adding SecureW2 JoinNow Connector from the gallery</span><span class="sxs-lookup"><span data-stu-id="f2f54-121">Adding SecureW2 JoinNow Connector from the gallery</span></span>
2. <span data-ttu-id="f2f54-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f2f54-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-securew2-joinnow-connector-from-the-gallery"></a><span data-ttu-id="f2f54-123">Adding SecureW2 JoinNow Connector from the gallery</span><span class="sxs-lookup"><span data-stu-id="f2f54-123">Adding SecureW2 JoinNow Connector from the gallery</span></span>
<span data-ttu-id="f2f54-124">To configure the integration of SecureW2 JoinNow Connector into Azure AD, you need to add SecureW2 JoinNow Connector from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f2f54-124">To configure the integration of SecureW2 JoinNow Connector into Azure AD, you need to add SecureW2 JoinNow Connector from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f2f54-125">**To add SecureW2 JoinNow Connector from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f2f54-125">**To add SecureW2 JoinNow Connector from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f2f54-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f2f54-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="f2f54-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="f2f54-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f2f54-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f2f54-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="f2f54-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="f2f54-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="f2f54-133">In the search box, type **SecureW2 JoinNow Connector**, select **SecureW2 JoinNow Connector** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="f2f54-133">In the search box, type **SecureW2 JoinNow Connector**, select **SecureW2 JoinNow Connector** from result panel then click **Add** button to add the application.</span></span>

    ![SecureW2 JoinNow Connector in the results list](./media/securejoinnow-tutorial/tutorial_securejoinnow_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f2f54-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f2f54-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f2f54-136">In this section, you configure and test Azure AD single sign-on with SecureW2 JoinNow Connector based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f2f54-136">In this section, you configure and test Azure AD single sign-on with SecureW2 JoinNow Connector based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f2f54-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SecureW2 JoinNow Connector is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f2f54-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SecureW2 JoinNow Connector is to a user in Azure AD.</span></span> <span data-ttu-id="f2f54-138">In other words, a link relationship between an Azure AD user and the related user in SecureW2 JoinNow Connector needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f2f54-138">In other words, a link relationship between an Azure AD user and the related user in SecureW2 JoinNow Connector needs to be established.</span></span>

<span data-ttu-id="f2f54-139">To configure and test Azure AD single sign-on with SecureW2 JoinNow Connector, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f2f54-139">To configure and test Azure AD single sign-on with SecureW2 JoinNow Connector, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f2f54-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f2f54-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f2f54-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f2f54-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f2f54-142">**[Create a SecureW2 JoinNow Connector test user](#create-a-securew2-joinnow-connector-test-user)** - to have a counterpart of Britta Simon in SecureW2 JoinNow Connector that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="f2f54-142">**[Create a SecureW2 JoinNow Connector test user](#create-a-securew2-joinnow-connector-test-user)** - to have a counterpart of Britta Simon in SecureW2 JoinNow Connector that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f2f54-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f2f54-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f2f54-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f2f54-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f2f54-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f2f54-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f2f54-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SecureW2 JoinNow Connector application.</span><span class="sxs-lookup"><span data-stu-id="f2f54-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SecureW2 JoinNow Connector application.</span></span>

<span data-ttu-id="f2f54-147">**To configure Azure AD single sign-on with SecureW2 JoinNow Connector, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f2f54-147">**To configure Azure AD single sign-on with SecureW2 JoinNow Connector, perform the following steps:**</span></span>

1. <span data-ttu-id="f2f54-148">In the Azure portal, on the **SecureW2 JoinNow Connector** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f2f54-148">In the Azure portal, on the **SecureW2 JoinNow Connector** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="f2f54-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f2f54-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/securejoinnow-tutorial/tutorial_securejoinnow_samlbase.png)

3. <span data-ttu-id="f2f54-152">On the **SecureW2 JoinNow Connector Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f2f54-152">On the **SecureW2 JoinNow Connector Domain and URLs** section, perform the following steps:</span></span>

    ![SecureW2 JoinNow Connector Domain and URLs single sign-on information](./media/securejoinnow-tutorial/tutorial_securejoinnow_url.png)

    <span data-ttu-id="f2f54-154">a.</span><span class="sxs-lookup"><span data-stu-id="f2f54-154">a.</span></span> <span data-ttu-id="f2f54-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<organization-identifier>-auth.securew2.com/auth/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="f2f54-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<organization-identifier>-auth.securew2.com/auth/saml/SSO`</span></span>

    <span data-ttu-id="f2f54-156">b.</span><span class="sxs-lookup"><span data-stu-id="f2f54-156">b.</span></span> <span data-ttu-id="f2f54-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<organization-identifier>-auth.securew2.com/auth/saml`</span><span class="sxs-lookup"><span data-stu-id="f2f54-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<organization-identifier>-auth.securew2.com/auth/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f2f54-158">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="f2f54-158">These values are not real.</span></span> <span data-ttu-id="f2f54-159">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="f2f54-159">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f2f54-160">Contact [SecureW2 JoinNow Connector Client support team](mailto:support@securew2.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="f2f54-160">Contact [SecureW2 JoinNow Connector Client support team](mailto:support@securew2.com) to get these values.</span></span> 

4. <span data-ttu-id="f2f54-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="f2f54-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/securejoinnow-tutorial/tutorial_securejoinnow_certificate.png) 

5. <span data-ttu-id="f2f54-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="f2f54-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/securejoinnow-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f2f54-165">To configure single sign-on on **SecureW2 JoinNow Connector** side, you need to send the downloaded **Metadata XML** to [SecureW2 JoinNow Connector support team](mailto:support@securew2.com).</span><span class="sxs-lookup"><span data-stu-id="f2f54-165">To configure single sign-on on **SecureW2 JoinNow Connector** side, you need to send the downloaded **Metadata XML** to [SecureW2 JoinNow Connector support team](mailto:support@securew2.com).</span></span> <span data-ttu-id="f2f54-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="f2f54-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f2f54-167">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f2f54-167">Create an Azure AD test user</span></span>

<span data-ttu-id="f2f54-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f2f54-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="f2f54-170">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f2f54-170">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f2f54-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="f2f54-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/securejoinnow-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f2f54-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="f2f54-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/securejoinnow-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f2f54-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="f2f54-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/securejoinnow-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f2f54-177">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f2f54-177">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/securejoinnow-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f2f54-179">a.</span><span class="sxs-lookup"><span data-stu-id="f2f54-179">a.</span></span> <span data-ttu-id="f2f54-180">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f2f54-180">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f2f54-181">b.</span><span class="sxs-lookup"><span data-stu-id="f2f54-181">b.</span></span> <span data-ttu-id="f2f54-182">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f2f54-182">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f2f54-183">c.</span><span class="sxs-lookup"><span data-stu-id="f2f54-183">c.</span></span> <span data-ttu-id="f2f54-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="f2f54-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f2f54-185">d.</span><span class="sxs-lookup"><span data-stu-id="f2f54-185">d.</span></span> <span data-ttu-id="f2f54-186">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f2f54-186">Click **Create**.</span></span>
 
### <a name="create-a-securew2-joinnow-connector-test-user"></a><span data-ttu-id="f2f54-187">Create a SecureW2 JoinNow Connector test user</span><span class="sxs-lookup"><span data-stu-id="f2f54-187">Create a SecureW2 JoinNow Connector test user</span></span>

<span data-ttu-id="f2f54-188">In this section, you create a user called Britta Simon in SecureW2 JoinNow Connector.</span><span class="sxs-lookup"><span data-stu-id="f2f54-188">In this section, you create a user called Britta Simon in SecureW2 JoinNow Connector.</span></span> <span data-ttu-id="f2f54-189">Work with [SecureW2 JoinNow Connector Client support team](mailto:support@securew2.com) to add the users in the SecureW2 JoinNow Connector platform.</span><span class="sxs-lookup"><span data-stu-id="f2f54-189">Work with [SecureW2 JoinNow Connector Client support team](mailto:support@securew2.com) to add the users in the SecureW2 JoinNow Connector platform.</span></span> <span data-ttu-id="f2f54-190">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f2f54-190">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f2f54-191">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f2f54-191">Assign the Azure AD test user</span></span>

<span data-ttu-id="f2f54-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SecureW2 JoinNow Connector.</span><span class="sxs-lookup"><span data-stu-id="f2f54-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SecureW2 JoinNow Connector.</span></span>

![Assign the user role][200] 

<span data-ttu-id="f2f54-194">**To assign Britta Simon to SecureW2 JoinNow Connector, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f2f54-194">**To assign Britta Simon to SecureW2 JoinNow Connector, perform the following steps:**</span></span>

1. <span data-ttu-id="f2f54-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f2f54-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="f2f54-197">In the applications list, select **SecureW2 JoinNow Connector**.</span><span class="sxs-lookup"><span data-stu-id="f2f54-197">In the applications list, select **SecureW2 JoinNow Connector**.</span></span>

    ![The SecureW2 JoinNow Connector link in the Applications list](./media/securejoinnow-tutorial/tutorial_securejoinnow_app.png)  

3. <span data-ttu-id="f2f54-199">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f2f54-199">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="f2f54-201">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="f2f54-201">Click **Add** button.</span></span> <span data-ttu-id="f2f54-202">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f2f54-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="f2f54-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="f2f54-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f2f54-205">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="f2f54-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f2f54-206">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f2f54-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f2f54-207">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="f2f54-207">Test single sign-on</span></span>

<span data-ttu-id="f2f54-208">**To test the application, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f2f54-208">**To test the application, perform the following steps:**</span></span> 

<span data-ttu-id="f2f54-209">a.</span><span class="sxs-lookup"><span data-stu-id="f2f54-209">a.</span></span> <span data-ttu-id="f2f54-210">Open the SecureW2 JoinNow Connector client, select your appropriate device from the list and click on **Sign In** button.</span><span class="sxs-lookup"><span data-stu-id="f2f54-210">Open the SecureW2 JoinNow Connector client, select your appropriate device from the list and click on **Sign In** button.</span></span>

<span data-ttu-id="f2f54-211">b.</span><span class="sxs-lookup"><span data-stu-id="f2f54-211">b.</span></span> <span data-ttu-id="f2f54-212">The default browser should open and you should be re-directed to the Azure portal for authentication.</span><span class="sxs-lookup"><span data-stu-id="f2f54-212">The default browser should open and you should be re-directed to the Azure portal for authentication.</span></span>

<span data-ttu-id="f2f54-213">c.</span><span class="sxs-lookup"><span data-stu-id="f2f54-213">c.</span></span> <span data-ttu-id="f2f54-214">On successful authentication, it should return back to the initial landing page of SecureW2 JoinNow Connector.</span><span class="sxs-lookup"><span data-stu-id="f2f54-214">On successful authentication, it should return back to the initial landing page of SecureW2 JoinNow Connector.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f2f54-215">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f2f54-215">Additional resources</span></span>

* [<span data-ttu-id="f2f54-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f2f54-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="f2f54-217">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f2f54-217">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/securejoinnow-tutorial/tutorial_general_01.png
[2]: ./media/securejoinnow-tutorial/tutorial_general_02.png
[3]: ./media/securejoinnow-tutorial/tutorial_general_03.png
[4]: ./media/securejoinnow-tutorial/tutorial_general_04.png

[100]: ./media/securejoinnow-tutorial/tutorial_general_100.png

[200]: ./media/securejoinnow-tutorial/tutorial_general_200.png
[201]: ./media/securejoinnow-tutorial/tutorial_general_201.png
[202]: ./media/securejoinnow-tutorial/tutorial_general_202.png
[203]: ./media/securejoinnow-tutorial/tutorial_general_203.png

