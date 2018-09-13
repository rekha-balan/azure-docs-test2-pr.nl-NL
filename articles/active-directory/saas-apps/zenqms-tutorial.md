---
title: 'Tutorial: Azure Active Directory integration with ZenQMS | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ZenQMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 72857c30-8896-438d-90c9-aeb21bf5fec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2018
ms.author: jeedes
ms.openlocfilehash: 57a8c698133b2b5516a1f5d352f28148afe6f3d2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865104"
---
# <a name="tutorial-azure-active-directory-integration-with-zenqms"></a><span data-ttu-id="7c9da-103">Tutorial: Azure Active Directory integration with ZenQMS</span><span class="sxs-lookup"><span data-stu-id="7c9da-103">Tutorial: Azure Active Directory integration with ZenQMS</span></span>

<span data-ttu-id="7c9da-104">In this tutorial, you learn how to integrate ZenQMS with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7c9da-104">In this tutorial, you learn how to integrate ZenQMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7c9da-105">Integrating ZenQMS with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7c9da-105">Integrating ZenQMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7c9da-106">You can control in Azure AD who has access to ZenQMS.</span><span class="sxs-lookup"><span data-stu-id="7c9da-106">You can control in Azure AD who has access to ZenQMS.</span></span>
- <span data-ttu-id="7c9da-107">You can enable your users to automatically get signed-on to ZenQMS (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="7c9da-107">You can enable your users to automatically get signed-on to ZenQMS (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7c9da-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7c9da-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="7c9da-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="7c9da-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c9da-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7c9da-110">Prerequisites</span></span>

<span data-ttu-id="7c9da-111">To configure Azure AD integration with ZenQMS, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7c9da-111">To configure Azure AD integration with ZenQMS, you need the following items:</span></span>

- <span data-ttu-id="7c9da-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7c9da-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7c9da-113">A ZenQMS single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7c9da-113">A ZenQMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7c9da-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7c9da-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7c9da-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7c9da-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7c9da-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="7c9da-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7c9da-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7c9da-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7c9da-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7c9da-118">Scenario description</span></span>

<span data-ttu-id="7c9da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7c9da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="7c9da-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7c9da-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7c9da-121">Adding ZenQMS from the gallery</span><span class="sxs-lookup"><span data-stu-id="7c9da-121">Adding ZenQMS from the gallery</span></span>
2. <span data-ttu-id="7c9da-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7c9da-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zenqms-from-the-gallery"></a><span data-ttu-id="7c9da-123">Adding ZenQMS from the gallery</span><span class="sxs-lookup"><span data-stu-id="7c9da-123">Adding ZenQMS from the gallery</span></span>

<span data-ttu-id="7c9da-124">To configure the integration of ZenQMS into Azure AD, you need to add ZenQMS from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7c9da-124">To configure the integration of ZenQMS into Azure AD, you need to add ZenQMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7c9da-125">**To add ZenQMS from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7c9da-125">**To add ZenQMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7c9da-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7c9da-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="7c9da-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="7c9da-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7c9da-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7c9da-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="7c9da-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="7c9da-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="7c9da-133">In the search box, type **ZenQMS**, select **ZenQMS** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="7c9da-133">In the search box, type **ZenQMS**, select **ZenQMS** from result panel then click **Add** button to add the application.</span></span>

    ![ZenQMS in the results list](./media/zenqms-tutorial/tutorial_zenqms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7c9da-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7c9da-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7c9da-136">In this section, you configure and test Azure AD single sign-on with ZenQMS based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7c9da-136">In this section, you configure and test Azure AD single sign-on with ZenQMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7c9da-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ZenQMS is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c9da-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ZenQMS is to a user in Azure AD.</span></span> <span data-ttu-id="7c9da-138">In other words, a link relationship between an Azure AD user and the related user in ZenQMS needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7c9da-138">In other words, a link relationship between an Azure AD user and the related user in ZenQMS needs to be established.</span></span>

<span data-ttu-id="7c9da-139">To configure and test Azure AD single sign-on with ZenQMS, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7c9da-139">To configure and test Azure AD single sign-on with ZenQMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7c9da-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7c9da-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7c9da-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7c9da-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7c9da-142">**[Create a ZenQMS test user](#create-a-zenqms-test-user)** - to have a counterpart of Britta Simon in ZenQMS that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="7c9da-142">**[Create a ZenQMS test user](#create-a-zenqms-test-user)** - to have a counterpart of Britta Simon in ZenQMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7c9da-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7c9da-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7c9da-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7c9da-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7c9da-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7c9da-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7c9da-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ZenQMS application.</span><span class="sxs-lookup"><span data-stu-id="7c9da-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ZenQMS application.</span></span>

<span data-ttu-id="7c9da-147">**To configure Azure AD single sign-on with ZenQMS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7c9da-147">**To configure Azure AD single sign-on with ZenQMS, perform the following steps:**</span></span>

1. <span data-ttu-id="7c9da-148">In the Azure portal, on the **ZenQMS** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7c9da-148">In the Azure portal, on the **ZenQMS** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="7c9da-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7c9da-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/zenqms-tutorial/tutorial_zenqms_samlbase.png)

3. <span data-ttu-id="7c9da-152">On the **ZenQMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="7c9da-152">On the **ZenQMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![ZenQMS Domain and URLs single sign-on information](./media/zenqms-tutorial/tutorial_zenqms_url.png)

    <span data-ttu-id="7c9da-154">a.</span><span class="sxs-lookup"><span data-stu-id="7c9da-154">a.</span></span> <span data-ttu-id="7c9da-155">In the **Identifier** textbox, type a URL using the following pattern: `urn:zenqms:<INSTANCE>`</span><span class="sxs-lookup"><span data-stu-id="7c9da-155">In the **Identifier** textbox, type a URL using the following pattern: `urn:zenqms:<INSTANCE>`</span></span>

    <span data-ttu-id="7c9da-156">b.</span><span class="sxs-lookup"><span data-stu-id="7c9da-156">b.</span></span> <span data-ttu-id="7c9da-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<INSTANCE>.zenqms.com/SAML/AssertionConsumerService`</span><span class="sxs-lookup"><span data-stu-id="7c9da-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<INSTANCE>.zenqms.com/SAML/AssertionConsumerService`</span></span>

4. <span data-ttu-id="7c9da-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="7c9da-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![ZenQMS Domain and URLs single sign-on information](./media/zenqms-tutorial/tutorial_zenqms_url1.png)

    <span data-ttu-id="7c9da-160">In the **Sign-on URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="7c9da-160">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |-|-|
    | `https://<INSTANCE>.zenqms.com/<ID>`|
    | `https://<INSTANCE>.zenqms.com/<EMAIL DOMAIN>/`|
    | |

    > [!NOTE]
    > <span data-ttu-id="7c9da-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="7c9da-161">These values are not real.</span></span> <span data-ttu-id="7c9da-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="7c9da-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="7c9da-163">Contact [ZenQMS Client support team](mailto:help@zenqms.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="7c9da-163">Contact [ZenQMS Client support team](mailto:help@zenqms.com) to get these values.</span></span>

5. <span data-ttu-id="7c9da-164">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into Notepad.</span><span class="sxs-lookup"><span data-stu-id="7c9da-164">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into Notepad.</span></span>

    ![The Certificate download link](./media/zenqms-tutorial/tutorial_zenqms_certificate.png) 

6. <span data-ttu-id="7c9da-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7c9da-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/zenqms-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="7c9da-168">To configure single sign-on on **ZenQMS** side, you need to send the **App Federation Metadata Url** to [ZenQMS support team](mailto:help@zenqms.com).</span><span class="sxs-lookup"><span data-stu-id="7c9da-168">To configure single sign-on on **ZenQMS** side, you need to send the **App Federation Metadata Url** to [ZenQMS support team](mailto:help@zenqms.com).</span></span> <span data-ttu-id="7c9da-169">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="7c9da-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7c9da-170">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7c9da-170">Create an Azure AD test user</span></span>

<span data-ttu-id="7c9da-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7c9da-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="7c9da-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7c9da-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7c9da-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="7c9da-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/zenqms-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7c9da-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="7c9da-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/zenqms-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7c9da-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="7c9da-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/zenqms-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7c9da-180">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7c9da-180">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/zenqms-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7c9da-182">a.</span><span class="sxs-lookup"><span data-stu-id="7c9da-182">a.</span></span> <span data-ttu-id="7c9da-183">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7c9da-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7c9da-184">b.</span><span class="sxs-lookup"><span data-stu-id="7c9da-184">b.</span></span> <span data-ttu-id="7c9da-185">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7c9da-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="7c9da-186">c.</span><span class="sxs-lookup"><span data-stu-id="7c9da-186">c.</span></span> <span data-ttu-id="7c9da-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="7c9da-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="7c9da-188">d.</span><span class="sxs-lookup"><span data-stu-id="7c9da-188">d.</span></span> <span data-ttu-id="7c9da-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7c9da-189">Click **Create**.</span></span>

### <a name="create-a-zenqms-test-user"></a><span data-ttu-id="7c9da-190">Create a ZenQMS test user</span><span class="sxs-lookup"><span data-stu-id="7c9da-190">Create a ZenQMS test user</span></span>

<span data-ttu-id="7c9da-191">In this section, you create a user called Britta Simon in ZenQMS.</span><span class="sxs-lookup"><span data-stu-id="7c9da-191">In this section, you create a user called Britta Simon in ZenQMS.</span></span> <span data-ttu-id="7c9da-192">Work with [ZenQMS support team](mailto:help@zenqms.com) to add the users in the ZenQMS platform.</span><span class="sxs-lookup"><span data-stu-id="7c9da-192">Work with [ZenQMS support team](mailto:help@zenqms.com) to add the users in the ZenQMS platform.</span></span> <span data-ttu-id="7c9da-193">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7c9da-193">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7c9da-194">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7c9da-194">Assign the Azure AD test user</span></span>

<span data-ttu-id="7c9da-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ZenQMS.</span><span class="sxs-lookup"><span data-stu-id="7c9da-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ZenQMS.</span></span>

![Assign the user role][200]

<span data-ttu-id="7c9da-197">**To assign Britta Simon to ZenQMS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7c9da-197">**To assign Britta Simon to ZenQMS, perform the following steps:**</span></span>

1. <span data-ttu-id="7c9da-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7c9da-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="7c9da-200">In the applications list, select **ZenQMS**.</span><span class="sxs-lookup"><span data-stu-id="7c9da-200">In the applications list, select **ZenQMS**.</span></span>

    ![The ZenQMS link in the Applications list](./media/zenqms-tutorial/tutorial_zenqms_app.png)  

3. <span data-ttu-id="7c9da-202">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="7c9da-202">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="7c9da-204">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="7c9da-204">Click **Add** button.</span></span> <span data-ttu-id="7c9da-205">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7c9da-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="7c9da-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="7c9da-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7c9da-208">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="7c9da-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7c9da-209">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7c9da-209">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="7c9da-210">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="7c9da-210">Test single sign-on</span></span>

<span data-ttu-id="7c9da-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7c9da-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7c9da-212">When you click the ZenQMS tile in the Access Panel, you should get automatically signed-on to your ZenQMS application.</span><span class="sxs-lookup"><span data-stu-id="7c9da-212">When you click the ZenQMS tile in the Access Panel, you should get automatically signed-on to your ZenQMS application.</span></span>
<span data-ttu-id="7c9da-213">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7c9da-213">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7c9da-214">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7c9da-214">Additional resources</span></span>

* [<span data-ttu-id="7c9da-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c9da-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="7c9da-216">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7c9da-216">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/zenqms-tutorial/tutorial_general_01.png
[2]: ./media/zenqms-tutorial/tutorial_general_02.png
[3]: ./media/zenqms-tutorial/tutorial_general_03.png
[4]: ./media/zenqms-tutorial/tutorial_general_04.png

[100]: ./media/zenqms-tutorial/tutorial_general_100.png

[200]: ./media/zenqms-tutorial/tutorial_general_200.png
[201]: ./media/zenqms-tutorial/tutorial_general_201.png
[202]: ./media/zenqms-tutorial/tutorial_general_202.png
[203]: ./media/zenqms-tutorial/tutorial_general_203.png
