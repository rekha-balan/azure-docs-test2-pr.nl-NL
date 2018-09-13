---
title: 'Tutorial: Azure Active Directory integration with Bpm’online | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Bpm’online.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 052db91d-ccff-4098-8ae3-2f76eca90539
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/16/2018
ms.author: jeedes
ms.openlocfilehash: b6fe50b24a20f81500ac1ed5008fcb6c59c0243a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866270"
---
# <a name="tutorial-azure-active-directory-integration-with-bpmonline"></a><span data-ttu-id="fed7e-103">Tutorial: Azure Active Directory integration with Bpm’online</span><span class="sxs-lookup"><span data-stu-id="fed7e-103">Tutorial: Azure Active Directory integration with Bpm’online</span></span>

<span data-ttu-id="fed7e-104">In this tutorial, you learn how to integrate Bpm’online with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fed7e-104">In this tutorial, you learn how to integrate Bpm’online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fed7e-105">Integrating Bpm’online with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="fed7e-105">Integrating Bpm’online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fed7e-106">You can control in Azure AD who has access to Bpm’online.</span><span class="sxs-lookup"><span data-stu-id="fed7e-106">You can control in Azure AD who has access to Bpm’online.</span></span>
- <span data-ttu-id="fed7e-107">You can enable your users to automatically get signed-on to Bpm’online (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="fed7e-107">You can enable your users to automatically get signed-on to Bpm’online (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fed7e-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fed7e-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="fed7e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="fed7e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fed7e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fed7e-110">Prerequisites</span></span>

<span data-ttu-id="fed7e-111">To configure Azure AD integration with Bpm’online, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="fed7e-111">To configure Azure AD integration with Bpm’online, you need the following items:</span></span>

- <span data-ttu-id="fed7e-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="fed7e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fed7e-113">A Bpm’online single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="fed7e-113">A Bpm’online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fed7e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="fed7e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fed7e-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="fed7e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fed7e-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="fed7e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fed7e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fed7e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fed7e-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="fed7e-118">Scenario description</span></span>
<span data-ttu-id="fed7e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="fed7e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fed7e-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="fed7e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fed7e-121">Adding Bpm’online from the gallery</span><span class="sxs-lookup"><span data-stu-id="fed7e-121">Adding Bpm’online from the gallery</span></span>
1. <span data-ttu-id="fed7e-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fed7e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bpmonline-from-the-gallery"></a><span data-ttu-id="fed7e-123">Adding Bpm’online from the gallery</span><span class="sxs-lookup"><span data-stu-id="fed7e-123">Adding Bpm’online from the gallery</span></span>
<span data-ttu-id="fed7e-124">To configure the integration of Bpm’online into Azure AD, you need to add Bpm’online from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="fed7e-124">To configure the integration of Bpm’online into Azure AD, you need to add Bpm’online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fed7e-125">**To add Bpm’online from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fed7e-125">**To add Bpm’online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fed7e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="fed7e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="fed7e-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="fed7e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fed7e-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="fed7e-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="fed7e-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="fed7e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="fed7e-133">In the search box, type **Bpm’online**, select **Bpm’online** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="fed7e-133">In the search box, type **Bpm’online**, select **Bpm’online** from result panel then click **Add** button to add the application.</span></span>

    ![Bpm’online in the results list](./media/bpmonline-tutorial/tutorial_bpmonline_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fed7e-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fed7e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fed7e-136">In this section, you configure and test Azure AD single sign-on with Bpm’online based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="fed7e-136">In this section, you configure and test Azure AD single sign-on with Bpm’online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fed7e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Bpm’online is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fed7e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Bpm’online is to a user in Azure AD.</span></span> <span data-ttu-id="fed7e-138">In other words, a link relationship between an Azure AD user and the related user in Bpm’online needs to be established.</span><span class="sxs-lookup"><span data-stu-id="fed7e-138">In other words, a link relationship between an Azure AD user and the related user in Bpm’online needs to be established.</span></span>

<span data-ttu-id="fed7e-139">In Bpm’online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="fed7e-139">In Bpm’online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fed7e-140">To configure and test Azure AD single sign-on with Bpm’online, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="fed7e-140">To configure and test Azure AD single sign-on with Bpm’online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fed7e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="fed7e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="fed7e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fed7e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="fed7e-143">**[Create a Bpm’online test user](#create-a-bpmonline-test-user)** - to have a counterpart of Britta Simon in Bpm’online that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="fed7e-143">**[Create a Bpm’online test user](#create-a-bpmonline-test-user)** - to have a counterpart of Britta Simon in Bpm’online that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="fed7e-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fed7e-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="fed7e-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="fed7e-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fed7e-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fed7e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fed7e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bpm’online application.</span><span class="sxs-lookup"><span data-stu-id="fed7e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bpm’online application.</span></span>

<span data-ttu-id="fed7e-148">**To configure Azure AD single sign-on with Bpm’online, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fed7e-148">**To configure Azure AD single sign-on with Bpm’online, perform the following steps:**</span></span>

1. <span data-ttu-id="fed7e-149">In the Azure portal, on the **Bpm’online** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="fed7e-149">In the Azure portal, on the **Bpm’online** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="fed7e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fed7e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/bpmonline-tutorial/tutorial_bpmonline_samlbase.png)

1. <span data-ttu-id="fed7e-153">On the **Bpm’online Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="fed7e-153">On the **Bpm’online Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Bpm’online Domain and URLs single sign-on information](./media/bpmonline-tutorial/tutorial_bpmonline_url.png)

    <span data-ttu-id="fed7e-155">a.</span><span class="sxs-lookup"><span data-stu-id="fed7e-155">a.</span></span> <span data-ttu-id="fed7e-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<client site name>.bpmonline.com/`</span><span class="sxs-lookup"><span data-stu-id="fed7e-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<client site name>.bpmonline.com/`</span></span>

    <span data-ttu-id="fed7e-157">b.</span><span class="sxs-lookup"><span data-stu-id="fed7e-157">b.</span></span> <span data-ttu-id="fed7e-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<client site name>.bpmonline.com/ServiceModel/AuthService.svc/SsoLogin`</span><span class="sxs-lookup"><span data-stu-id="fed7e-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<client site name>.bpmonline.com/ServiceModel/AuthService.svc/SsoLogin`</span></span>

1. <span data-ttu-id="fed7e-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="fed7e-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Bpm’online Domain and URLs single sign-on information](./media/bpmonline-tutorial/tutorial_bpmonline_url1.png)

    <span data-ttu-id="fed7e-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<client site name>.bpmonline.com/`</span><span class="sxs-lookup"><span data-stu-id="fed7e-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<client site name>.bpmonline.com/`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="fed7e-162">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="fed7e-162">These values are not real.</span></span> <span data-ttu-id="fed7e-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="fed7e-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="fed7e-164">Contact [Bpm’online Client support team](mailto:support@bpmonline.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="fed7e-164">Contact [Bpm’online Client support team](mailto:support@bpmonline.com) to get these values.</span></span> 

1. <span data-ttu-id="fed7e-165">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="fed7e-165">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>
    
    ![Configure Single Sign-On](./media/bpmonline-tutorial/tutorial_metadataurl.png)
     
1. <span data-ttu-id="fed7e-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="fed7e-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/bpmonline-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="fed7e-169">To configure single sign-on on **Bpm’online** side, you need to send the **App Federation Metadata Url** to [Bpm’online support team](mailto:support@bpmonline.com).</span><span class="sxs-lookup"><span data-stu-id="fed7e-169">To configure single sign-on on **Bpm’online** side, you need to send the **App Federation Metadata Url** to [Bpm’online support team](mailto:support@bpmonline.com).</span></span> <span data-ttu-id="fed7e-170">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="fed7e-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fed7e-171">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="fed7e-171">Create an Azure AD test user</span></span>

<span data-ttu-id="fed7e-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fed7e-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="fed7e-174">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fed7e-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fed7e-175">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="fed7e-175">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/bpmonline-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="fed7e-177">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="fed7e-177">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/bpmonline-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="fed7e-179">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="fed7e-179">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/bpmonline-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="fed7e-181">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fed7e-181">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/bpmonline-tutorial/create_aaduser_04.png)

    <span data-ttu-id="fed7e-183">a.</span><span class="sxs-lookup"><span data-stu-id="fed7e-183">a.</span></span> <span data-ttu-id="fed7e-184">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fed7e-184">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fed7e-185">b.</span><span class="sxs-lookup"><span data-stu-id="fed7e-185">b.</span></span> <span data-ttu-id="fed7e-186">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fed7e-186">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="fed7e-187">c.</span><span class="sxs-lookup"><span data-stu-id="fed7e-187">c.</span></span> <span data-ttu-id="fed7e-188">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="fed7e-188">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="fed7e-189">d.</span><span class="sxs-lookup"><span data-stu-id="fed7e-189">d.</span></span> <span data-ttu-id="fed7e-190">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="fed7e-190">Click **Create**.</span></span>
 
### <a name="create-a-bpmonline-test-user"></a><span data-ttu-id="fed7e-191">Create a Bpm’online test user</span><span class="sxs-lookup"><span data-stu-id="fed7e-191">Create a Bpm’online test user</span></span>

<span data-ttu-id="fed7e-192">In this section, you create a user called Britta Simon in Bpm’online.</span><span class="sxs-lookup"><span data-stu-id="fed7e-192">In this section, you create a user called Britta Simon in Bpm’online.</span></span> <span data-ttu-id="fed7e-193">Work with [Bpm’online support team](mailto:support@bpmonline.com) to add the users in the Bpm’online platform.</span><span class="sxs-lookup"><span data-stu-id="fed7e-193">Work with [Bpm’online support team](mailto:support@bpmonline.com) to add the users in the Bpm’online platform.</span></span> <span data-ttu-id="fed7e-194">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fed7e-194">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="fed7e-195">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="fed7e-195">Assign the Azure AD test user</span></span>

<span data-ttu-id="fed7e-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bpm’online.</span><span class="sxs-lookup"><span data-stu-id="fed7e-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bpm’online.</span></span>

![Assign the user role][200] 

<span data-ttu-id="fed7e-198">**To assign Britta Simon to Bpm’online, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fed7e-198">**To assign Britta Simon to Bpm’online, perform the following steps:**</span></span>

1. <span data-ttu-id="fed7e-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="fed7e-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="fed7e-201">In the applications list, select **Bpm’online**.</span><span class="sxs-lookup"><span data-stu-id="fed7e-201">In the applications list, select **Bpm’online**.</span></span>

    ![The Bpm’online link in the Applications list](./media/bpmonline-tutorial/tutorial_bpmonline_app.png)  

1. <span data-ttu-id="fed7e-203">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="fed7e-203">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="fed7e-205">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="fed7e-205">Click **Add** button.</span></span> <span data-ttu-id="fed7e-206">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="fed7e-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="fed7e-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="fed7e-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="fed7e-209">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="fed7e-209">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="fed7e-210">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="fed7e-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fed7e-211">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="fed7e-211">Test single sign-on</span></span>

<span data-ttu-id="fed7e-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="fed7e-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fed7e-213">When you click the Bpm’online tile in the Access Panel, you should get automatically signed-on to your Bpm’online application.</span><span class="sxs-lookup"><span data-stu-id="fed7e-213">When you click the Bpm’online tile in the Access Panel, you should get automatically signed-on to your Bpm’online application.</span></span>
<span data-ttu-id="fed7e-214">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fed7e-214">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fed7e-215">Additional resources</span><span class="sxs-lookup"><span data-stu-id="fed7e-215">Additional resources</span></span>

* [<span data-ttu-id="fed7e-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fed7e-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="fed7e-217">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fed7e-217">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/bpmonline-tutorial/tutorial_general_01.png
[2]: ./media/bpmonline-tutorial/tutorial_general_02.png
[3]: ./media/bpmonline-tutorial/tutorial_general_03.png
[4]: ./media/bpmonline-tutorial/tutorial_general_04.png

[100]: ./media/bpmonline-tutorial/tutorial_general_100.png

[200]: ./media/bpmonline-tutorial/tutorial_general_200.png
[201]: ./media/bpmonline-tutorial/tutorial_general_201.png
[202]: ./media/bpmonline-tutorial/tutorial_general_202.png
[203]: ./media/bpmonline-tutorial/tutorial_general_203.png

