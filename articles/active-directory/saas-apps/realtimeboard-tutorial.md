---
title: 'Tutorial: Azure Active Directory integration with RealtimeBoard | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and RealtimeBoard.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: a37fc1c0-4bae-4173-989b-00de53a0076f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: jeedes
ms.openlocfilehash: 00b0844deb8cc81f770f6c98f8b020f1402d2ff7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857966"
---
# <a name="tutorial-azure-active-directory-integration-with-realtimeboard"></a><span data-ttu-id="b9f1f-103">Tutorial: Azure Active Directory integration with RealtimeBoard</span><span class="sxs-lookup"><span data-stu-id="b9f1f-103">Tutorial: Azure Active Directory integration with RealtimeBoard</span></span>

<span data-ttu-id="b9f1f-104">In this tutorial, you learn how to integrate RealtimeBoard with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b9f1f-104">In this tutorial, you learn how to integrate RealtimeBoard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9f1f-105">Integrating RealtimeBoard with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="b9f1f-105">Integrating RealtimeBoard with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b9f1f-106">You can control in Azure AD who has access to RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-106">You can control in Azure AD who has access to RealtimeBoard.</span></span>
- <span data-ttu-id="b9f1f-107">You can enable your users to automatically get signed-on to RealtimeBoard (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-107">You can enable your users to automatically get signed-on to RealtimeBoard (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b9f1f-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b9f1f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="b9f1f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9f1f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b9f1f-110">Prerequisites</span></span>

<span data-ttu-id="b9f1f-111">To configure Azure AD integration with RealtimeBoard, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="b9f1f-111">To configure Azure AD integration with RealtimeBoard, you need the following items:</span></span>

- <span data-ttu-id="b9f1f-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="b9f1f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9f1f-113">A RealtimeBoard single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b9f1f-113">A RealtimeBoard single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9f1f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9f1f-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="b9f1f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9f1f-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b9f1f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9f1f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9f1f-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="b9f1f-118">Scenario description</span></span>
<span data-ttu-id="b9f1f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9f1f-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="b9f1f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9f1f-121">Adding RealtimeBoard from the gallery</span><span class="sxs-lookup"><span data-stu-id="b9f1f-121">Adding RealtimeBoard from the gallery</span></span>
2. <span data-ttu-id="b9f1f-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b9f1f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-realtimeboard-from-the-gallery"></a><span data-ttu-id="b9f1f-123">Adding RealtimeBoard from the gallery</span><span class="sxs-lookup"><span data-stu-id="b9f1f-123">Adding RealtimeBoard from the gallery</span></span>
<span data-ttu-id="b9f1f-124">To configure the integration of RealtimeBoard into Azure AD, you need to add RealtimeBoard from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-124">To configure the integration of RealtimeBoard into Azure AD, you need to add RealtimeBoard from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b9f1f-125">**To add RealtimeBoard from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b9f1f-125">**To add RealtimeBoard from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b9f1f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="b9f1f-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b9f1f-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="b9f1f-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="b9f1f-133">In the search box, type **RealtimeBoard**, select **RealtimeBoard** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-133">In the search box, type **RealtimeBoard**, select **RealtimeBoard** from result panel then click **Add** button to add the application.</span></span>

    ![RealtimeBoard in the results list](./media/realtimeboard-tutorial/tutorial_realtimeboard_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b9f1f-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b9f1f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b9f1f-136">In this section, you configure and test Azure AD single sign-on with RealtimeBoard based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b9f1f-136">In this section, you configure and test Azure AD single sign-on with RealtimeBoard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b9f1f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in RealtimeBoard is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in RealtimeBoard is to a user in Azure AD.</span></span> <span data-ttu-id="b9f1f-138">In other words, a link relationship between an Azure AD user and the related user in RealtimeBoard needs to be established.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-138">In other words, a link relationship between an Azure AD user and the related user in RealtimeBoard needs to be established.</span></span>

<span data-ttu-id="b9f1f-139">In RealtimeBoard, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-139">In RealtimeBoard, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b9f1f-140">To configure and test Azure AD single sign-on with RealtimeBoard, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b9f1f-140">To configure and test Azure AD single sign-on with RealtimeBoard, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b9f1f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b9f1f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9f1f-143">**[Create a RealtimeBoard test user](#create-a-realtimeboard-test-user)** - to have a counterpart of Britta Simon in RealtimeBoard that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-143">**[Create a RealtimeBoard test user](#create-a-realtimeboard-test-user)** - to have a counterpart of Britta Simon in RealtimeBoard that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b9f1f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9f1f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b9f1f-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b9f1f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b9f1f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RealtimeBoard application.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RealtimeBoard application.</span></span>

<span data-ttu-id="b9f1f-148">**To configure Azure AD single sign-on with RealtimeBoard, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b9f1f-148">**To configure Azure AD single sign-on with RealtimeBoard, perform the following steps:**</span></span>

1. <span data-ttu-id="b9f1f-149">In the Azure portal, on the **RealtimeBoard** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-149">In the Azure portal, on the **RealtimeBoard** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="b9f1f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/realtimeboard-tutorial/tutorial_realtimeboard_samlbase.png)

3. <span data-ttu-id="b9f1f-153">On the **RealtimeBoard Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="b9f1f-153">On the **RealtimeBoard Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![RealtimeBoard Domain and URLs single sign-on information](./media/realtimeboard-tutorial/tutorial_realtimeboard_url.png)

    <span data-ttu-id="b9f1f-155">In the **Identifier** textbox, type a URL as: `https://realtimeboard.com/`</span><span class="sxs-lookup"><span data-stu-id="b9f1f-155">In the **Identifier** textbox, type a URL as: `https://realtimeboard.com/`</span></span>

4. <span data-ttu-id="b9f1f-156">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="b9f1f-156">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/realtimeboard-tutorial/tutorial_realtimeboard_url2.png)

    <span data-ttu-id="b9f1f-158">In the **Sign-on URL** textbox, type a URL as: `https://realtimeboard.com/sso/saml`</span><span class="sxs-lookup"><span data-stu-id="b9f1f-158">In the **Sign-on URL** textbox, type a URL as: `https://realtimeboard.com/sso/saml`</span></span>

5. <span data-ttu-id="b9f1f-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/realtimeboard-tutorial/tutorial_realtimeboard_certificate.png) 

6. <span data-ttu-id="b9f1f-161">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-161">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/realtimeboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="b9f1f-163">To configure single sign-on on the **RealtimeBoard** side, follow the [RealtimeBoard instructions](https://help.realtimeboard.com/support/solutions/articles/11000023465-saml-based-single-sign-on-), and use the data from your downloaded **Metadata XML**.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-163">To configure single sign-on on the **RealtimeBoard** side, follow the [RealtimeBoard instructions](https://help.realtimeboard.com/support/solutions/articles/11000023465-saml-based-single-sign-on-), and use the data from your downloaded **Metadata XML**.</span></span>

> [!TIP]
> <span data-ttu-id="b9f1f-164">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="b9f1f-164">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b9f1f-165">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-165">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b9f1f-166">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b9f1f-166">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b9f1f-167">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b9f1f-167">Create an Azure AD test user</span></span>

<span data-ttu-id="b9f1f-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="b9f1f-170">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b9f1f-170">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b9f1f-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/realtimeboard-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b9f1f-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/realtimeboard-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b9f1f-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/realtimeboard-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b9f1f-177">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b9f1f-177">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/realtimeboard-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b9f1f-179">a.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-179">a.</span></span> <span data-ttu-id="b9f1f-180">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-180">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9f1f-181">b.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-181">b.</span></span> <span data-ttu-id="b9f1f-182">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-182">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b9f1f-183">c.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-183">c.</span></span> <span data-ttu-id="b9f1f-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b9f1f-185">d.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-185">d.</span></span> <span data-ttu-id="b9f1f-186">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-186">Click **Create**.</span></span>
 
### <a name="create-a-realtimeboard-test-user"></a><span data-ttu-id="b9f1f-187">Create a RealtimeBoard test user</span><span class="sxs-lookup"><span data-stu-id="b9f1f-187">Create a RealtimeBoard test user</span></span>

<span data-ttu-id="b9f1f-188">The objective of this section is to create a user called Britta Simon in RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-188">The objective of this section is to create a user called Britta Simon in RealtimeBoard.</span></span> <span data-ttu-id="b9f1f-189">RealtimeBoard supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-189">RealtimeBoard supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="b9f1f-190">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-190">There is no action item for you in this section.</span></span> <span data-ttu-id="b9f1f-191">If a user doesn't already exist in RealtimeBoard, a new one is created when you attempt to access RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-191">If a user doesn't already exist in RealtimeBoard, a new one is created when you attempt to access RealtimeBoard.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b9f1f-192">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b9f1f-192">Assign the Azure AD test user</span></span>

<span data-ttu-id="b9f1f-193">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-193">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RealtimeBoard.</span></span>

![Assign the user role][200] 

<span data-ttu-id="b9f1f-195">**To assign Britta Simon to RealtimeBoard, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b9f1f-195">**To assign Britta Simon to RealtimeBoard, perform the following steps:**</span></span>

1. <span data-ttu-id="b9f1f-196">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-196">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="b9f1f-198">In the applications list, select **RealtimeBoard**.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-198">In the applications list, select **RealtimeBoard**.</span></span>

    ![The RealtimeBoard link in the Applications list](./media/realtimeboard-tutorial/tutorial_realtimeboard_app.png)  

3. <span data-ttu-id="b9f1f-200">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-200">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="b9f1f-202">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-202">Click **Add** button.</span></span> <span data-ttu-id="b9f1f-203">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="b9f1f-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b9f1f-206">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b9f1f-207">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b9f1f-208">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="b9f1f-208">Test single sign-on</span></span>

<span data-ttu-id="b9f1f-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b9f1f-210">When you click the RealtimeBoard tile in the Access Panel, you should get automatically signed-on to your RealtimeBoard application.</span><span class="sxs-lookup"><span data-stu-id="b9f1f-210">When you click the RealtimeBoard tile in the Access Panel, you should get automatically signed-on to your RealtimeBoard application.</span></span>
<span data-ttu-id="b9f1f-211">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b9f1f-211">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b9f1f-212">Additional resources</span><span class="sxs-lookup"><span data-stu-id="b9f1f-212">Additional resources</span></span>

* [<span data-ttu-id="b9f1f-213">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9f1f-213">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="b9f1f-214">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b9f1f-214">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/realtimeboard-tutorial/tutorial_general_01.png
[2]: ./media/realtimeboard-tutorial/tutorial_general_02.png
[3]: ./media/realtimeboard-tutorial/tutorial_general_03.png
[4]: ./media/realtimeboard-tutorial/tutorial_general_04.png

[100]: ./media/realtimeboard-tutorial/tutorial_general_100.png

[200]: ./media/realtimeboard-tutorial/tutorial_general_200.png
[201]: ./media/realtimeboard-tutorial/tutorial_general_201.png
[202]: ./media/realtimeboard-tutorial/tutorial_general_202.png
[203]: ./media/realtimeboard-tutorial/tutorial_general_203.png

