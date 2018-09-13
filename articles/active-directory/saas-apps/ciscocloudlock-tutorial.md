---
title: 'Tutorial: Azure Active Directory integration with The Cloud Security Fabric | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and The Cloud Security Fabric.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 549e8810-1b3b-4351-bf4b-f07de98980d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2018
ms.author: jeedes
ms.openlocfilehash: 9908dae627ae11a42e8e01a9a4f4d11f35ce0f8d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867227"
---
# <a name="tutorial-azure-active-directory-integration-with-the-cloud-security-fabric"></a><span data-ttu-id="ae0ef-103">Tutorial: Azure Active Directory integration with The Cloud Security Fabric</span><span class="sxs-lookup"><span data-stu-id="ae0ef-103">Tutorial: Azure Active Directory integration with The Cloud Security Fabric</span></span>

<span data-ttu-id="ae0ef-104">In this tutorial, you learn how to integrate The Cloud Security Fabric with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae0ef-104">In this tutorial, you learn how to integrate The Cloud Security Fabric with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae0ef-105">Integrating The Cloud Security Fabric with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ae0ef-105">Integrating The Cloud Security Fabric with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ae0ef-106">You can control in Azure AD who has access to The Cloud Security Fabric.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-106">You can control in Azure AD who has access to The Cloud Security Fabric.</span></span>
- <span data-ttu-id="ae0ef-107">You can enable your users to automatically get signed-on to The Cloud Security Fabric (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-107">You can enable your users to automatically get signed-on to The Cloud Security Fabric (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ae0ef-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="ae0ef-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="ae0ef-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae0ef-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ae0ef-110">Prerequisites</span></span>

<span data-ttu-id="ae0ef-111">To configure Azure AD integration with The Cloud Security Fabric, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ae0ef-111">To configure Azure AD integration with The Cloud Security Fabric, you need the following items:</span></span>

- <span data-ttu-id="ae0ef-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ae0ef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae0ef-113">A The Cloud Security Fabric single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ae0ef-113">A The Cloud Security Fabric single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ae0ef-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ae0ef-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ae0ef-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae0ef-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ae0ef-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae0ef-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae0ef-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="ae0ef-118">Scenario description</span></span>
<span data-ttu-id="ae0ef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae0ef-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ae0ef-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae0ef-121">Adding The Cloud Security Fabric from the gallery</span><span class="sxs-lookup"><span data-stu-id="ae0ef-121">Adding The Cloud Security Fabric from the gallery</span></span>
1. <span data-ttu-id="ae0ef-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ae0ef-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-the-cloud-security-fabric-from-the-gallery"></a><span data-ttu-id="ae0ef-123">Adding The Cloud Security Fabric from the gallery</span><span class="sxs-lookup"><span data-stu-id="ae0ef-123">Adding The Cloud Security Fabric from the gallery</span></span>
<span data-ttu-id="ae0ef-124">To configure the integration of The Cloud Security Fabric into Azure AD, you need to add The Cloud Security Fabric from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-124">To configure the integration of The Cloud Security Fabric into Azure AD, you need to add The Cloud Security Fabric from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ae0ef-125">**To add The Cloud Security Fabric from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae0ef-125">**To add The Cloud Security Fabric from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ae0ef-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="ae0ef-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ae0ef-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="ae0ef-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="ae0ef-133">In the search box, type **The Cloud Security Fabric**, select **The Cloud Security Fabric** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-133">In the search box, type **The Cloud Security Fabric**, select **The Cloud Security Fabric** from result panel then click **Add** button to add the application.</span></span>

    ![The Cloud Security Fabric in the results list](./media/ciscocloudlock-tutorial/tutorial_ciscocloudlock_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ae0ef-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ae0ef-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ae0ef-136">In this section, you configure and test Azure AD single sign-on with The Cloud Security Fabric based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ae0ef-136">In this section, you configure and test Azure AD single sign-on with The Cloud Security Fabric based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ae0ef-137">For single sign-on to work, Azure AD needs to know what the counterpart user in The Cloud Security Fabric is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-137">For single sign-on to work, Azure AD needs to know what the counterpart user in The Cloud Security Fabric is to a user in Azure AD.</span></span> <span data-ttu-id="ae0ef-138">In other words, a link relationship between an Azure AD user and the related user in The Cloud Security Fabric needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-138">In other words, a link relationship between an Azure AD user and the related user in The Cloud Security Fabric needs to be established.</span></span>

<span data-ttu-id="ae0ef-139">To configure and test Azure AD single sign-on with The Cloud Security Fabric, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ae0ef-139">To configure and test Azure AD single sign-on with The Cloud Security Fabric, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ae0ef-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="ae0ef-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="ae0ef-142">**[Create a The Cloud Security Fabric test user](#create-a-the-cloud-security-fabric-test-user)** - to have a counterpart of Britta Simon in The Cloud Security Fabric that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-142">**[Create a The Cloud Security Fabric test user](#create-a-the-cloud-security-fabric-test-user)** - to have a counterpart of Britta Simon in The Cloud Security Fabric that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="ae0ef-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="ae0ef-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ae0ef-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ae0ef-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ae0ef-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your The Cloud Security Fabric application.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your The Cloud Security Fabric application.</span></span>

<span data-ttu-id="ae0ef-147">**To configure Azure AD single sign-on with The Cloud Security Fabric, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae0ef-147">**To configure Azure AD single sign-on with The Cloud Security Fabric, perform the following steps:**</span></span>

1. <span data-ttu-id="ae0ef-148">In the Azure portal, on the **The Cloud Security Fabric** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-148">In the Azure portal, on the **The Cloud Security Fabric** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="ae0ef-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/ciscocloudlock-tutorial/tutorial_ciscocloudlock_samlbase.png)

1. <span data-ttu-id="ae0ef-152">On the **The Cloud Security Fabric Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ae0ef-152">On the **The Cloud Security Fabric Domain and URLs** section, perform the following steps:</span></span>

    ![The Cloud Security Fabric Domain and URLs single sign-on information](./media/ciscocloudlock-tutorial/tutorial_ciscocloudlock_url.png)

    <span data-ttu-id="ae0ef-154">a.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-154">a.</span></span> <span data-ttu-id="ae0ef-155">In the **Sign-on URL** textbox, type a URL:</span><span class="sxs-lookup"><span data-stu-id="ae0ef-155">In the **Sign-on URL** textbox, type a URL:</span></span>
    | |
    |--|
    | `https://platform.cloudlock.com` |
    | `https://app.cloudlock.com` |

    <span data-ttu-id="ae0ef-156">b.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-156">b.</span></span> <span data-ttu-id="ae0ef-157">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="ae0ef-157">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://platform.cloudlock.com/gate/saml/sso/<subdomain>` |
    | `https://app.cloudlock.com/gate/saml/sso/<subdomain>` |

    > [!NOTE]
    > <span data-ttu-id="ae0ef-158">The Identifier value is not real.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-158">The Identifier value is not real.</span></span> <span data-ttu-id="ae0ef-159">Update the value with the actual Identifier.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-159">Update the value with the actual Identifier.</span></span> <span data-ttu-id="ae0ef-160">Contact [The Cloud Security Fabric Client support team](mailto:support@cloudlock.com) to get the value.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-160">Contact [The Cloud Security Fabric Client support team](mailto:support@cloudlock.com) to get the value.</span></span> 

1. <span data-ttu-id="ae0ef-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/ciscocloudlock-tutorial/tutorial_ciscocloudlock_certificate.png)

1. <span data-ttu-id="ae0ef-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/ciscocloudlock-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="ae0ef-165">To configure single sign-on on **The Cloud Security Fabric** side, you need to send the downloaded **Metadata XML** to [The Cloud Security Fabric support team](mailto:support@cloudlock.com).</span><span class="sxs-lookup"><span data-stu-id="ae0ef-165">To configure single sign-on on **The Cloud Security Fabric** side, you need to send the downloaded **Metadata XML** to [The Cloud Security Fabric support team](mailto:support@cloudlock.com).</span></span> <span data-ttu-id="ae0ef-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ae0ef-167">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ae0ef-167">Create an Azure AD test user</span></span>

<span data-ttu-id="ae0ef-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="ae0ef-170">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae0ef-170">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ae0ef-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/ciscocloudlock-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="ae0ef-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/ciscocloudlock-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="ae0ef-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/ciscocloudlock-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="ae0ef-177">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ae0ef-177">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/ciscocloudlock-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ae0ef-179">a.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-179">a.</span></span> <span data-ttu-id="ae0ef-180">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-180">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae0ef-181">b.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-181">b.</span></span> <span data-ttu-id="ae0ef-182">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-182">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="ae0ef-183">c.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-183">c.</span></span> <span data-ttu-id="ae0ef-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="ae0ef-185">d.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-185">d.</span></span> <span data-ttu-id="ae0ef-186">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-186">Click **Create**.</span></span>

### <a name="create-a-the-cloud-security-fabric-test-user"></a><span data-ttu-id="ae0ef-187">Create a The Cloud Security Fabric test user</span><span class="sxs-lookup"><span data-stu-id="ae0ef-187">Create a The Cloud Security Fabric test user</span></span>

<span data-ttu-id="ae0ef-188">In this section, you create a user called Britta Simon in The Cloud Security Fabric.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-188">In this section, you create a user called Britta Simon in The Cloud Security Fabric.</span></span> <span data-ttu-id="ae0ef-189">Work with [The Cloud Security Fabric support team](mailto:support@cloudlock.com) to add the users in The Cloud Security Fabric platform.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-189">Work with [The Cloud Security Fabric support team](mailto:support@cloudlock.com) to add the users in The Cloud Security Fabric platform.</span></span> <span data-ttu-id="ae0ef-190">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-190">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ae0ef-191">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ae0ef-191">Assign the Azure AD test user</span></span>

<span data-ttu-id="ae0ef-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to The Cloud Security Fabric.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to The Cloud Security Fabric.</span></span>

![Assign the user role][200]

<span data-ttu-id="ae0ef-194">**To assign Britta Simon to The Cloud Security Fabric, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae0ef-194">**To assign Britta Simon to The Cloud Security Fabric, perform the following steps:**</span></span>

1. <span data-ttu-id="ae0ef-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

1. <span data-ttu-id="ae0ef-197">In the applications list, select **The Cloud Security Fabric**.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-197">In the applications list, select **The Cloud Security Fabric**.</span></span>

    ![The Cloud Security Fabric link in the Applications list](./media/ciscocloudlock-tutorial/tutorial_ciscocloudlock_app.png)  

1. <span data-ttu-id="ae0ef-199">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-199">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="ae0ef-201">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-201">Click **Add** button.</span></span> <span data-ttu-id="ae0ef-202">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="ae0ef-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="ae0ef-205">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-205">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="ae0ef-206">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-206">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="ae0ef-207">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="ae0ef-207">Test single sign-on</span></span>

<span data-ttu-id="ae0ef-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ae0ef-209">When you click The Cloud Security Fabric tile in the Access Panel, you should get automatically signed-on to your The Cloud Security Fabric application.</span><span class="sxs-lookup"><span data-stu-id="ae0ef-209">When you click The Cloud Security Fabric tile in the Access Panel, you should get automatically signed-on to your The Cloud Security Fabric application.</span></span>
<span data-ttu-id="ae0ef-210">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ae0ef-210">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae0ef-211">Additional resources</span><span class="sxs-lookup"><span data-stu-id="ae0ef-211">Additional resources</span></span>

* [<span data-ttu-id="ae0ef-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae0ef-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="ae0ef-213">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ae0ef-213">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/ciscocloudlock-tutorial/tutorial_general_01.png
[2]: ./media/ciscocloudlock-tutorial/tutorial_general_02.png
[3]: ./media/ciscocloudlock-tutorial/tutorial_general_03.png
[4]: ./media/ciscocloudlock-tutorial/tutorial_general_04.png

[100]: ./media/ciscocloudlock-tutorial/tutorial_general_100.png

[200]: ./media/ciscocloudlock-tutorial/tutorial_general_200.png
[201]: ./media/ciscocloudlock-tutorial/tutorial_general_201.png
[202]: ./media/ciscocloudlock-tutorial/tutorial_general_202.png
[203]: ./media/ciscocloudlock-tutorial/tutorial_general_203.png
