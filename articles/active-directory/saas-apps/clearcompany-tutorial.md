---
title: 'Tutorial: Azure Active Directory integration with ClearCompany | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ClearCompany.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 2819da18-c7eb-43cf-aac3-1403a540bf6e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: jeedes
ms.openlocfilehash: 0463a89b8c320b31929bf5e0322079088c2cdeab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856851"
---
# <a name="tutorial-azure-active-directory-integration-with-clearcompany"></a><span data-ttu-id="95088-103">Tutorial: Azure Active Directory integration with ClearCompany</span><span class="sxs-lookup"><span data-stu-id="95088-103">Tutorial: Azure Active Directory integration with ClearCompany</span></span>

<span data-ttu-id="95088-104">In this tutorial, you learn how to integrate ClearCompany with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="95088-104">In this tutorial, you learn how to integrate ClearCompany with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="95088-105">Integrating ClearCompany with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="95088-105">Integrating ClearCompany with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="95088-106">You can control in Azure AD who has access to ClearCompany.</span><span class="sxs-lookup"><span data-stu-id="95088-106">You can control in Azure AD who has access to ClearCompany.</span></span>
- <span data-ttu-id="95088-107">You can enable your users to automatically get signed-on to ClearCompany (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="95088-107">You can enable your users to automatically get signed-on to ClearCompany (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="95088-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="95088-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="95088-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="95088-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95088-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="95088-110">Prerequisites</span></span>

<span data-ttu-id="95088-111">To configure Azure AD integration with ClearCompany, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="95088-111">To configure Azure AD integration with ClearCompany, you need the following items:</span></span>

- <span data-ttu-id="95088-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="95088-112">An Azure AD subscription</span></span>
- <span data-ttu-id="95088-113">A ClearCompany single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="95088-113">A ClearCompany single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="95088-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="95088-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="95088-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="95088-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="95088-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="95088-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="95088-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="95088-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="95088-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="95088-118">Scenario description</span></span>
<span data-ttu-id="95088-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="95088-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="95088-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="95088-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="95088-121">Adding ClearCompany from the gallery</span><span class="sxs-lookup"><span data-stu-id="95088-121">Adding ClearCompany from the gallery</span></span>
2. <span data-ttu-id="95088-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="95088-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clearcompany-from-the-gallery"></a><span data-ttu-id="95088-123">Adding ClearCompany from the gallery</span><span class="sxs-lookup"><span data-stu-id="95088-123">Adding ClearCompany from the gallery</span></span>
<span data-ttu-id="95088-124">To configure the integration of ClearCompany into Azure AD, you need to add ClearCompany from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="95088-124">To configure the integration of ClearCompany into Azure AD, you need to add ClearCompany from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="95088-125">**To add ClearCompany from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="95088-125">**To add ClearCompany from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="95088-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="95088-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="95088-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="95088-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="95088-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="95088-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="95088-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="95088-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="95088-133">In the search box, type **ClearCompany**, select **ClearCompany** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="95088-133">In the search box, type **ClearCompany**, select **ClearCompany** from result panel then click **Add** button to add the application.</span></span>

    ![ClearCompany in the results list](./media/clearcompany-tutorial/tutorial_clearcompany_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="95088-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="95088-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="95088-136">In this section, you configure and test Azure AD single sign-on with ClearCompany based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="95088-136">In this section, you configure and test Azure AD single sign-on with ClearCompany based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="95088-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ClearCompany is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95088-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ClearCompany is to a user in Azure AD.</span></span> <span data-ttu-id="95088-138">In other words, a link relationship between an Azure AD user and the related user in ClearCompany needs to be established.</span><span class="sxs-lookup"><span data-stu-id="95088-138">In other words, a link relationship between an Azure AD user and the related user in ClearCompany needs to be established.</span></span>

<span data-ttu-id="95088-139">In ClearCompany, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="95088-139">In ClearCompany, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="95088-140">To configure and test Azure AD single sign-on with ClearCompany, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="95088-140">To configure and test Azure AD single sign-on with ClearCompany, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="95088-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="95088-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="95088-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="95088-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="95088-143">**[Create a ClearCompany test user](#create-a-clearcompany-test-user)** - to have a counterpart of Britta Simon in ClearCompany that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="95088-143">**[Create a ClearCompany test user](#create-a-clearcompany-test-user)** - to have a counterpart of Britta Simon in ClearCompany that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="95088-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="95088-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="95088-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="95088-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="95088-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="95088-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="95088-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ClearCompany application.</span><span class="sxs-lookup"><span data-stu-id="95088-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ClearCompany application.</span></span>

<span data-ttu-id="95088-148">**To configure Azure AD single sign-on with ClearCompany, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="95088-148">**To configure Azure AD single sign-on with ClearCompany, perform the following steps:**</span></span>

1. <span data-ttu-id="95088-149">In the Azure portal, on the **ClearCompany** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="95088-149">In the Azure portal, on the **ClearCompany** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="95088-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="95088-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/clearcompany-tutorial/tutorial_clearcompany_samlbase.png)

3. <span data-ttu-id="95088-153">On the **ClearCompany Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span><span class="sxs-lookup"><span data-stu-id="95088-153">On the **ClearCompany Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![ClearCompany Domain and URLs single sign-on information](./media/clearcompany-tutorial/tutorial_clearcompany_url1.png)

    <span data-ttu-id="95088-155">In the **Identifier** textbox, type the URL: `https://api.clearcompany.com`</span><span class="sxs-lookup"><span data-stu-id="95088-155">In the **Identifier** textbox, type the URL: `https://api.clearcompany.com`</span></span>

4. <span data-ttu-id="95088-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="95088-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![ClearCompany Domain and URLs single sign-on information](./media/clearcompany-tutorial/tutorial_clearcompany_url2.png)

    <span data-ttu-id="95088-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.clearcompany.com`</span><span class="sxs-lookup"><span data-stu-id="95088-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.clearcompany.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="95088-159">Sign-on URL value is not a real value.</span><span class="sxs-lookup"><span data-stu-id="95088-159">Sign-on URL value is not a real value.</span></span> <span data-ttu-id="95088-160">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="95088-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="95088-161">Contact [ClearCompany Client support team](http://www.clearcompany.com/support) to get this value.</span><span class="sxs-lookup"><span data-stu-id="95088-161">Contact [ClearCompany Client support team](http://www.clearcompany.com/support) to get this value.</span></span> 

5. <span data-ttu-id="95088-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="95088-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/clearcompany-tutorial/tutorial_clearcompany_certificate.png) 

6. <span data-ttu-id="95088-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="95088-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/clearcompany-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="95088-166">On the **ClearCompany Configuration** section, click **Configure ClearCompany** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="95088-166">On the **ClearCompany Configuration** section, click **Configure ClearCompany** to open **Configure sign-on** window.</span></span> <span data-ttu-id="95088-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="95088-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![ClearCompany Configuration](./media/clearcompany-tutorial/tutorial_clearcompany_configure.png) 

8. <span data-ttu-id="95088-169">To configure single sign-on on **ClearCompany** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [ClearCompany support team](http://www.clearcompany.com/support).</span><span class="sxs-lookup"><span data-stu-id="95088-169">To configure single sign-on on **ClearCompany** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [ClearCompany support team](http://www.clearcompany.com/support).</span></span> <span data-ttu-id="95088-170">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="95088-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="95088-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="95088-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="95088-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="95088-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="95088-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="95088-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="95088-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="95088-174">Create an Azure AD test user</span></span>

<span data-ttu-id="95088-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="95088-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="95088-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="95088-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="95088-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="95088-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/clearcompany-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="95088-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="95088-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/clearcompany-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="95088-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="95088-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/clearcompany-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="95088-184">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="95088-184">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/clearcompany-tutorial/create_aaduser_04.png)

    <span data-ttu-id="95088-186">a.</span><span class="sxs-lookup"><span data-stu-id="95088-186">a.</span></span> <span data-ttu-id="95088-187">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="95088-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="95088-188">b.</span><span class="sxs-lookup"><span data-stu-id="95088-188">b.</span></span> <span data-ttu-id="95088-189">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="95088-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="95088-190">c.</span><span class="sxs-lookup"><span data-stu-id="95088-190">c.</span></span> <span data-ttu-id="95088-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="95088-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="95088-192">d.</span><span class="sxs-lookup"><span data-stu-id="95088-192">d.</span></span> <span data-ttu-id="95088-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="95088-193">Click **Create**.</span></span>
 
### <a name="create-a-clearcompany-test-user"></a><span data-ttu-id="95088-194">Create a ClearCompany test user</span><span class="sxs-lookup"><span data-stu-id="95088-194">Create a ClearCompany test user</span></span>

<span data-ttu-id="95088-195">In this section, you create a user called Britta Simon in ClearCompany.</span><span class="sxs-lookup"><span data-stu-id="95088-195">In this section, you create a user called Britta Simon in ClearCompany.</span></span> <span data-ttu-id="95088-196">Work with [ClearCompany support team](http://www.clearcompany.com/support) to add the users in the ClearCompany platform.</span><span class="sxs-lookup"><span data-stu-id="95088-196">Work with [ClearCompany support team](http://www.clearcompany.com/support) to add the users in the ClearCompany platform.</span></span> <span data-ttu-id="95088-197">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="95088-197">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="95088-198">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="95088-198">Assign the Azure AD test user</span></span>

<span data-ttu-id="95088-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ClearCompany.</span><span class="sxs-lookup"><span data-stu-id="95088-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ClearCompany.</span></span>

![Assign the user role][200] 

<span data-ttu-id="95088-201">**To assign Britta Simon to ClearCompany, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="95088-201">**To assign Britta Simon to ClearCompany, perform the following steps:**</span></span>

1. <span data-ttu-id="95088-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="95088-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="95088-204">In the applications list, select **ClearCompany**.</span><span class="sxs-lookup"><span data-stu-id="95088-204">In the applications list, select **ClearCompany**.</span></span>

    ![The ClearCompany link in the Applications list](./media/clearcompany-tutorial/tutorial_clearcompany_app.png)  

3. <span data-ttu-id="95088-206">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="95088-206">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="95088-208">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="95088-208">Click **Add** button.</span></span> <span data-ttu-id="95088-209">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="95088-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="95088-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="95088-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="95088-212">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="95088-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="95088-213">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="95088-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="95088-214">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="95088-214">Test single sign-on</span></span>

<span data-ttu-id="95088-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="95088-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="95088-216">When you click the ClearCompany tile in the Access Panel, you should get automatically signed-on to your ClearCompany application.</span><span class="sxs-lookup"><span data-stu-id="95088-216">When you click the ClearCompany tile in the Access Panel, you should get automatically signed-on to your ClearCompany application.</span></span>
<span data-ttu-id="95088-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="95088-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="95088-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="95088-218">Additional resources</span></span>

* [<span data-ttu-id="95088-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="95088-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="95088-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="95088-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/clearcompany-tutorial/tutorial_general_01.png
[2]: ./media/clearcompany-tutorial/tutorial_general_02.png
[3]: ./media/clearcompany-tutorial/tutorial_general_03.png
[4]: ./media/clearcompany-tutorial/tutorial_general_04.png

[100]: ./media/clearcompany-tutorial/tutorial_general_100.png

[200]: ./media/clearcompany-tutorial/tutorial_general_200.png
[201]: ./media/clearcompany-tutorial/tutorial_general_201.png
[202]: ./media/clearcompany-tutorial/tutorial_general_202.png
[203]: ./media/clearcompany-tutorial/tutorial_general_203.png

