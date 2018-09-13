---
title: 'Tutorial: Azure Active Directory integration with Compliance ELF | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Compliance ELF.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69c6efc3-54c7-49ec-b827-33177c09aa13
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/16/2018
ms.author: jeedes
ms.openlocfilehash: e5a7bfc51bcd1931def202d701127de701afb595
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867588"
---
# <a name="tutorial-azure-active-directory-integration-with-compliance-elf"></a><span data-ttu-id="7582b-103">Tutorial: Azure Active Directory integration with Compliance ELF</span><span class="sxs-lookup"><span data-stu-id="7582b-103">Tutorial: Azure Active Directory integration with Compliance ELF</span></span>

<span data-ttu-id="7582b-104">In this tutorial, you learn how to integrate Compliance ELF with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7582b-104">In this tutorial, you learn how to integrate Compliance ELF with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7582b-105">Integrating Compliance ELF with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7582b-105">Integrating Compliance ELF with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7582b-106">You can control in Azure AD who has access to Compliance ELF.</span><span class="sxs-lookup"><span data-stu-id="7582b-106">You can control in Azure AD who has access to Compliance ELF.</span></span>
- <span data-ttu-id="7582b-107">You can enable your users to automatically get signed-on to Compliance ELF (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="7582b-107">You can enable your users to automatically get signed-on to Compliance ELF (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7582b-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7582b-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="7582b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="7582b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7582b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7582b-110">Prerequisites</span></span>

<span data-ttu-id="7582b-111">To configure Azure AD integration with Compliance ELF, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7582b-111">To configure Azure AD integration with Compliance ELF, you need the following items:</span></span>

- <span data-ttu-id="7582b-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7582b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7582b-113">A Compliance ELF single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7582b-113">A Compliance ELF single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7582b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7582b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7582b-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7582b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7582b-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="7582b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7582b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7582b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7582b-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7582b-118">Scenario description</span></span>
<span data-ttu-id="7582b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7582b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7582b-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7582b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7582b-121">Adding Compliance ELF from the gallery</span><span class="sxs-lookup"><span data-stu-id="7582b-121">Adding Compliance ELF from the gallery</span></span>
2. <span data-ttu-id="7582b-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7582b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-compliance-elf-from-the-gallery"></a><span data-ttu-id="7582b-123">Adding Compliance ELF from the gallery</span><span class="sxs-lookup"><span data-stu-id="7582b-123">Adding Compliance ELF from the gallery</span></span>
<span data-ttu-id="7582b-124">To configure the integration of Compliance ELF into Azure AD, you need to add Compliance ELF from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7582b-124">To configure the integration of Compliance ELF into Azure AD, you need to add Compliance ELF from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7582b-125">**To add Compliance ELF from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7582b-125">**To add Compliance ELF from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7582b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7582b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="7582b-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="7582b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7582b-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7582b-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="7582b-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="7582b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="7582b-133">In the search box, type **Compliance ELF**, select **Compliance ELF** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="7582b-133">In the search box, type **Compliance ELF**, select **Compliance ELF** from result panel then click **Add** button to add the application.</span></span>

    ![Compliance ELF in the results list](./media/complianceelf-tutorial/tutorial_complianceelf_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7582b-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7582b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7582b-136">In this section, you configure and test Azure AD single sign-on with Compliance ELF based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7582b-136">In this section, you configure and test Azure AD single sign-on with Compliance ELF based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7582b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Compliance ELF is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7582b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Compliance ELF is to a user in Azure AD.</span></span> <span data-ttu-id="7582b-138">In other words, a link relationship between an Azure AD user and the related user in Compliance ELF needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7582b-138">In other words, a link relationship between an Azure AD user and the related user in Compliance ELF needs to be established.</span></span>

<span data-ttu-id="7582b-139">In Compliance ELF, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="7582b-139">In Compliance ELF, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7582b-140">To configure and test Azure AD single sign-on with Compliance ELF, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7582b-140">To configure and test Azure AD single sign-on with Compliance ELF, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7582b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7582b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7582b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7582b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7582b-143">**[Create a Compliance ELF test user](#create-a-compliance-elf-test-user)** - to have a counterpart of Britta Simon in Compliance ELF that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="7582b-143">**[Create a Compliance ELF test user](#create-a-compliance-elf-test-user)** - to have a counterpart of Britta Simon in Compliance ELF that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7582b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7582b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7582b-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7582b-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7582b-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7582b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7582b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Compliance ELF application.</span><span class="sxs-lookup"><span data-stu-id="7582b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Compliance ELF application.</span></span>

<span data-ttu-id="7582b-148">**To configure Azure AD single sign-on with Compliance ELF, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7582b-148">**To configure Azure AD single sign-on with Compliance ELF, perform the following steps:**</span></span>

1. <span data-ttu-id="7582b-149">In the Azure portal, on the **Compliance ELF** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7582b-149">In the Azure portal, on the **Compliance ELF** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="7582b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7582b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/complianceelf-tutorial/tutorial_complianceelf_samlbase.png)

3. <span data-ttu-id="7582b-153">On the **Compliance ELF Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="7582b-153">On the **Compliance ELF Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Compliance ELF Domain and URLs single sign-on information](./media/complianceelf-tutorial/tutorial_complianceelf_url.png)

    <span data-ttu-id="7582b-155">In the **Identifier** textbox, type a URL as: `https://sso.cordium.com`</span><span class="sxs-lookup"><span data-stu-id="7582b-155">In the **Identifier** textbox, type a URL as: `https://sso.cordium.com`</span></span>

4. <span data-ttu-id="7582b-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="7582b-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Compliance ELF Domain and URLs single sign-on](./media/complianceelf-tutorial/tutorial_complianceelf_url1.png)

    <span data-ttu-id="7582b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.complianceelf.com`</span><span class="sxs-lookup"><span data-stu-id="7582b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.complianceelf.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="7582b-159">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="7582b-159">This value is not real.</span></span> <span data-ttu-id="7582b-160">Update this values with the actual Sign-on URL.</span><span class="sxs-lookup"><span data-stu-id="7582b-160">Update this values with the actual Sign-on URL.</span></span> <span data-ttu-id="7582b-161">Contact [Compliance ELF support team](mailto:support@complianceelf.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="7582b-161">Contact [Compliance ELF support team](mailto:support@complianceelf.com) to get this value.</span></span>

5. <span data-ttu-id="7582b-162">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="7582b-162">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>
    
    ![Configure Single Sign-On](./media/complianceelf-tutorial/tutorial_metadataurl.png)
     
6. <span data-ttu-id="7582b-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7582b-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/complianceelf-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="7582b-166">To configure single sign-on on **Compliance ELF** side, you need to send the **App Federation Metadata Url** to [Compliance ELF support team](mailto:support@complianceelf.com).</span><span class="sxs-lookup"><span data-stu-id="7582b-166">To configure single sign-on on **Compliance ELF** side, you need to send the **App Federation Metadata Url** to [Compliance ELF support team](mailto:support@complianceelf.com).</span></span> <span data-ttu-id="7582b-167">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="7582b-167">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7582b-168">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7582b-168">Create an Azure AD test user</span></span>

<span data-ttu-id="7582b-169">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7582b-169">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="7582b-171">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7582b-171">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7582b-172">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="7582b-172">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/complianceelf-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7582b-174">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="7582b-174">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/complianceelf-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7582b-176">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="7582b-176">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/complianceelf-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7582b-178">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7582b-178">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/complianceelf-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7582b-180">a.</span><span class="sxs-lookup"><span data-stu-id="7582b-180">a.</span></span> <span data-ttu-id="7582b-181">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7582b-181">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7582b-182">b.</span><span class="sxs-lookup"><span data-stu-id="7582b-182">b.</span></span> <span data-ttu-id="7582b-183">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7582b-183">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="7582b-184">c.</span><span class="sxs-lookup"><span data-stu-id="7582b-184">c.</span></span> <span data-ttu-id="7582b-185">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="7582b-185">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="7582b-186">d.</span><span class="sxs-lookup"><span data-stu-id="7582b-186">d.</span></span> <span data-ttu-id="7582b-187">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7582b-187">Click **Create**.</span></span>
  
### <a name="create-a-compliance-elf-test-user"></a><span data-ttu-id="7582b-188">Create a Compliance ELF test user</span><span class="sxs-lookup"><span data-stu-id="7582b-188">Create a Compliance ELF test user</span></span>

<span data-ttu-id="7582b-189">In this section, you create a user called Britta Simon in Compliance ELF.</span><span class="sxs-lookup"><span data-stu-id="7582b-189">In this section, you create a user called Britta Simon in Compliance ELF.</span></span> <span data-ttu-id="7582b-190">Work with [Compliance ELF support team](mailto:support@complianceelf.com) to add the users in the Compliance ELF platform.</span><span class="sxs-lookup"><span data-stu-id="7582b-190">Work with [Compliance ELF support team](mailto:support@complianceelf.com) to add the users in the Compliance ELF platform.</span></span> <span data-ttu-id="7582b-191">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7582b-191">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7582b-192">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7582b-192">Assign the Azure AD test user</span></span>

<span data-ttu-id="7582b-193">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Compliance ELF.</span><span class="sxs-lookup"><span data-stu-id="7582b-193">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Compliance ELF.</span></span>

![Assign the user role][200] 

<span data-ttu-id="7582b-195">**To assign Britta Simon to Compliance ELF, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7582b-195">**To assign Britta Simon to Compliance ELF, perform the following steps:**</span></span>

1. <span data-ttu-id="7582b-196">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7582b-196">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="7582b-198">In the applications list, select **Compliance ELF**.</span><span class="sxs-lookup"><span data-stu-id="7582b-198">In the applications list, select **Compliance ELF**.</span></span>

    ![The Compliance ELF link in the Applications list](./media/complianceelf-tutorial/tutorial_complianceelf_app.png)  

3. <span data-ttu-id="7582b-200">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="7582b-200">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="7582b-202">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="7582b-202">Click **Add** button.</span></span> <span data-ttu-id="7582b-203">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7582b-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="7582b-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="7582b-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7582b-206">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="7582b-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7582b-207">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7582b-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7582b-208">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="7582b-208">Test single sign-on</span></span>

<span data-ttu-id="7582b-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7582b-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7582b-210">When you click the Compliance ELF tile in the Access Panel, you should get automatically signed-on to your Compliance ELF application.</span><span class="sxs-lookup"><span data-stu-id="7582b-210">When you click the Compliance ELF tile in the Access Panel, you should get automatically signed-on to your Compliance ELF application.</span></span>
<span data-ttu-id="7582b-211">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7582b-211">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7582b-212">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7582b-212">Additional resources</span></span>

* [<span data-ttu-id="7582b-213">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7582b-213">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="7582b-214">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7582b-214">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/complianceelf-tutorial/tutorial_general_01.png
[2]: ./media/complianceelf-tutorial/tutorial_general_02.png
[3]: ./media/complianceelf-tutorial/tutorial_general_03.png
[4]: ./media/complianceelf-tutorial/tutorial_general_04.png

[100]: ./media/complianceelf-tutorial/tutorial_general_100.png

[200]: ./media/complianceelf-tutorial/tutorial_general_200.png
[201]: ./media/complianceelf-tutorial/tutorial_general_201.png
[202]: ./media/complianceelf-tutorial/tutorial_general_202.png
[203]: ./media/complianceelf-tutorial/tutorial_general_203.png

