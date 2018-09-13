---
title: 'Tutorial: Azure Active Directory integration with YouEarnedIt | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and YouEarnedIt.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 3011d44d-dfcf-4061-888f-cff90fbc8150
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2018
ms.author: jeedes
ms.openlocfilehash: 3a394c13092547991bf7f8ae98e5c69e92077701
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864980"
---
# <a name="tutorial-azure-active-directory-integration-with-youearnedit"></a><span data-ttu-id="8e820-103">Tutorial: Azure Active Directory integration with YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="8e820-103">Tutorial: Azure Active Directory integration with YouEarnedIt</span></span>

<span data-ttu-id="8e820-104">In this tutorial, you learn how to integrate YouEarnedIt with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8e820-104">In this tutorial, you learn how to integrate YouEarnedIt with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8e820-105">Integrating YouEarnedIt with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8e820-105">Integrating YouEarnedIt with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8e820-106">You can control in Azure AD who has access to YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="8e820-106">You can control in Azure AD who has access to YouEarnedIt.</span></span>
- <span data-ttu-id="8e820-107">You can enable your users to automatically get signed-on to YouEarnedIt (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="8e820-107">You can enable your users to automatically get signed-on to YouEarnedIt (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8e820-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8e820-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="8e820-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="8e820-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e820-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8e820-110">Prerequisites</span></span>

<span data-ttu-id="8e820-111">To configure Azure AD integration with YouEarnedIt, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8e820-111">To configure Azure AD integration with YouEarnedIt, you need the following items:</span></span>

- <span data-ttu-id="8e820-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8e820-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8e820-113">A YouEarnedIt single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8e820-113">A YouEarnedIt single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8e820-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8e820-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8e820-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8e820-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8e820-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="8e820-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8e820-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8e820-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8e820-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8e820-118">Scenario description</span></span>

<span data-ttu-id="8e820-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8e820-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8e820-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8e820-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8e820-121">Adding YouEarnedIt from the gallery</span><span class="sxs-lookup"><span data-stu-id="8e820-121">Adding YouEarnedIt from the gallery</span></span>
2. <span data-ttu-id="8e820-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8e820-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-youearnedit-from-the-gallery"></a><span data-ttu-id="8e820-123">Adding YouEarnedIt from the gallery</span><span class="sxs-lookup"><span data-stu-id="8e820-123">Adding YouEarnedIt from the gallery</span></span>

<span data-ttu-id="8e820-124">To configure the integration of YouEarnedIt into Azure AD, you need to add YouEarnedIt from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8e820-124">To configure the integration of YouEarnedIt into Azure AD, you need to add YouEarnedIt from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8e820-125">**To add YouEarnedIt from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8e820-125">**To add YouEarnedIt from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8e820-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8e820-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="8e820-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="8e820-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8e820-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8e820-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="8e820-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="8e820-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="8e820-133">In the search box, type **YouEarnedt**, select  **YouEarnedt**  from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="8e820-133">In the search box, type **YouEarnedt**, select  **YouEarnedt**  from result panel then click **Add** button to add the application.</span></span>

    ![YouEarnedIt in the results list](./media/youearnedit-tutorial/tutorial_youearnedit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8e820-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8e820-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8e820-136">In this section, you configure and test Azure AD single sign-on with YouEarnedIt based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8e820-136">In this section, you configure and test Azure AD single sign-on with YouEarnedIt based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8e820-137">For single sign-on to work, Azure AD needs to know what the counterpart user in YouEarnedIt is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e820-137">For single sign-on to work, Azure AD needs to know what the counterpart user in YouEarnedIt is to a user in Azure AD.</span></span> <span data-ttu-id="8e820-138">In other words, a link relationship between an Azure AD user and the related user in YouEarnedIt needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8e820-138">In other words, a link relationship between an Azure AD user and the related user in YouEarnedIt needs to be established.</span></span>

<span data-ttu-id="8e820-139">In YouEarnedIt, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="8e820-139">In YouEarnedIt, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8e820-140">To configure and test Azure AD single sign-on with YouEarnedIt, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8e820-140">To configure and test Azure AD single sign-on with YouEarnedIt, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8e820-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8e820-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8e820-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e820-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8e820-143">**[Create a YouEarnedIt test user](#create-a-youearnedit-test-user)** - to have a counterpart of Britta Simon in YouEarnedIt that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="8e820-143">**[Create a YouEarnedIt test user](#create-a-youearnedit-test-user)** - to have a counterpart of Britta Simon in YouEarnedIt that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8e820-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8e820-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8e820-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8e820-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8e820-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8e820-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8e820-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your YouEarnedIt application.</span><span class="sxs-lookup"><span data-stu-id="8e820-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your YouEarnedIt application.</span></span>

<span data-ttu-id="8e820-148">**To configure Azure AD single sign-on with YouEarnedIt, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8e820-148">**To configure Azure AD single sign-on with YouEarnedIt, perform the following steps:**</span></span>

1. <span data-ttu-id="8e820-149">In the Azure portal, on the **YouEarnedIt** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8e820-149">In the Azure portal, on the **YouEarnedIt** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="8e820-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8e820-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/youearnedit-tutorial/tutorial_youearnedit_samlbase.png)

3. <span data-ttu-id="8e820-153">On the **YouEarnedIt Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8e820-153">On the **YouEarnedIt Domain and URLs** section, perform the following steps:</span></span>

    ![YouEarnedIt Domain and URLs single sign-on information](./media/youearnedit-tutorial/tutorial_youearnedit_url.png)

    <span data-ttu-id="8e820-155">a.</span><span class="sxs-lookup"><span data-stu-id="8e820-155">a.</span></span> <span data-ttu-id="8e820-156">In the **Sign-on URL** textbox, type a URL using the following patterns:</span><span class="sxs-lookup"><span data-stu-id="8e820-156">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    | <span data-ttu-id="8e820-157">Environment</span><span class="sxs-lookup"><span data-stu-id="8e820-157">Environment</span></span>  | <span data-ttu-id="8e820-158">Pattern</span><span class="sxs-lookup"><span data-stu-id="8e820-158">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="8e820-159">Production</span><span class="sxs-lookup"><span data-stu-id="8e820-159">Production</span></span> | `https://<company name>.youearnedit.com/users/sign_in` |
    | <span data-ttu-id="8e820-160">Sandbox</span><span class="sxs-lookup"><span data-stu-id="8e820-160">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com/users/sign_in` |

    <span data-ttu-id="8e820-161">b.</span><span class="sxs-lookup"><span data-stu-id="8e820-161">b.</span></span> <span data-ttu-id="8e820-162">In the **Identifier** textbox, type a URL using the following patterns:</span><span class="sxs-lookup"><span data-stu-id="8e820-162">In the **Identifier** textbox, type a URL using the following patterns:</span></span>
    | <span data-ttu-id="8e820-163">Environment</span><span class="sxs-lookup"><span data-stu-id="8e820-163">Environment</span></span>  | <span data-ttu-id="8e820-164">Pattern</span><span class="sxs-lookup"><span data-stu-id="8e820-164">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="8e820-165">Production</span><span class="sxs-lookup"><span data-stu-id="8e820-165">Production</span></span> | `https://<company name>.youearnedit.com` |
    | <span data-ttu-id="8e820-166">Sandbox</span><span class="sxs-lookup"><span data-stu-id="8e820-166">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com` |

    > [!NOTE] 
    > <span data-ttu-id="8e820-167">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="8e820-167">These values are not real.</span></span> <span data-ttu-id="8e820-168">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="8e820-168">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8e820-169">Contact your assigned YouEarnedIt Customer Success manager to get these values.</span><span class="sxs-lookup"><span data-stu-id="8e820-169">Contact your assigned YouEarnedIt Customer Success manager to get these values.</span></span>

4. <span data-ttu-id="8e820-170">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8e820-170">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/youearnedit-tutorial/tutorial_youearnedit_certificate.png) 

5. <span data-ttu-id="8e820-172">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="8e820-172">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/youearnedit-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8e820-174">On the **YouEarnedIt Configuration** section, click **Configure YouEarnedIt** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="8e820-174">On the **YouEarnedIt Configuration** section, click **Configure YouEarnedIt** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8e820-175">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="8e820-175">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![YouEarnedIt Configuration](./media/youearnedit-tutorial/tutorial_youearnedit_configure.png) 

7. <span data-ttu-id="8e820-177">To configure single sign-on on the **YouEarnedIt** side, you need to send the downloaded ***Certificate(Base64)*** and ***SAML Single Sign-On Service URL*** to your assigned **YouEarnedIt** Customer Success manager.</span><span class="sxs-lookup"><span data-stu-id="8e820-177">To configure single sign-on on the **YouEarnedIt** side, you need to send the downloaded ***Certificate(Base64)*** and ***SAML Single Sign-On Service URL*** to your assigned **YouEarnedIt** Customer Success manager.</span></span> <span data-ttu-id="8e820-178">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="8e820-178">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8e820-179">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8e820-179">Create an Azure AD test user</span></span>

<span data-ttu-id="8e820-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e820-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="8e820-182">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8e820-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8e820-183">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="8e820-183">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/youearnedit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="8e820-185">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="8e820-185">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/youearnedit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="8e820-187">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="8e820-187">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/youearnedit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="8e820-189">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8e820-189">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/youearnedit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8e820-191">a.</span><span class="sxs-lookup"><span data-stu-id="8e820-191">a.</span></span> <span data-ttu-id="8e820-192">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8e820-192">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8e820-193">b.</span><span class="sxs-lookup"><span data-stu-id="8e820-193">b.</span></span> <span data-ttu-id="8e820-194">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e820-194">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="8e820-195">c.</span><span class="sxs-lookup"><span data-stu-id="8e820-195">c.</span></span> <span data-ttu-id="8e820-196">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="8e820-196">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="8e820-197">d.</span><span class="sxs-lookup"><span data-stu-id="8e820-197">d.</span></span> <span data-ttu-id="8e820-198">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8e820-198">Click **Create**.</span></span>

### <a name="create-a-youearnedit-test-user"></a><span data-ttu-id="8e820-199">Create a YouEarnedIt test user</span><span class="sxs-lookup"><span data-stu-id="8e820-199">Create a YouEarnedIt test user</span></span>

<span data-ttu-id="8e820-200">In this section, you create a user called Britta Simon in YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="8e820-200">In this section, you create a user called Britta Simon in YouEarnedIt.</span></span> <span data-ttu-id="8e820-201">Please work with  your assigned YouEarnedIt Customer Success manager to add the users in the YouEarnedIt platform.</span><span class="sxs-lookup"><span data-stu-id="8e820-201">Please work with  your assigned YouEarnedIt Customer Success manager to add the users in the YouEarnedIt platform.</span></span>

>[!NOTE]
><span data-ttu-id="8e820-202">YouEarnedIt expect the Identity Provider to supply an EmailAddress  or UserName in the NameID attribute.</span><span class="sxs-lookup"><span data-stu-id="8e820-202">YouEarnedIt expect the Identity Provider to supply an EmailAddress  or UserName in the NameID attribute.</span></span> <span data-ttu-id="8e820-203">Authentication will fail if a corresponding UserName or EmailAddress is not found within the database or does not match exactly.</span><span class="sxs-lookup"><span data-stu-id="8e820-203">Authentication will fail if a corresponding UserName or EmailAddress is not found within the database or does not match exactly.</span></span> <span data-ttu-id="8e820-204">This will require that accounts be imported into the YouEarnedIt system before the SSO integration (Typically either via API or CSV import).</span><span class="sxs-lookup"><span data-stu-id="8e820-204">This will require that accounts be imported into the YouEarnedIt system before the SSO integration (Typically either via API or CSV import).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8e820-205">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8e820-205">Assign the Azure AD test user</span></span>

<span data-ttu-id="8e820-206">In this section, you enable Britta Simon to use Azure single sign-on by granting access to YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="8e820-206">In this section, you enable Britta Simon to use Azure single sign-on by granting access to YouEarnedIt.</span></span>

![Assign the user role][200]

<span data-ttu-id="8e820-208">**To assign Britta Simon to YouEarnedIt, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8e820-208">**To assign Britta Simon to YouEarnedIt, perform the following steps:**</span></span>

1. <span data-ttu-id="8e820-209">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8e820-209">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="8e820-211">In the applications list, select **YouEarnedIt**.</span><span class="sxs-lookup"><span data-stu-id="8e820-211">In the applications list, select **YouEarnedIt**.</span></span>

    ![The YouEarnedIt link in the Applications list](./media/youearnedit-tutorial/tutorial_youearnedit_app.png)  

3. <span data-ttu-id="8e820-213">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="8e820-213">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="8e820-215">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="8e820-215">Click **Add** button.</span></span> <span data-ttu-id="8e820-216">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8e820-216">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="8e820-218">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="8e820-218">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8e820-219">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="8e820-219">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8e820-220">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8e820-220">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="8e820-221">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="8e820-221">Test single sign-on</span></span>

<span data-ttu-id="8e820-222">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8e820-222">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8e820-223">When you click the YouEarnedIt tile in the Access Panel, you should get automatically signed-on to your YouEarnedIt application.</span><span class="sxs-lookup"><span data-stu-id="8e820-223">When you click the YouEarnedIt tile in the Access Panel, you should get automatically signed-on to your YouEarnedIt application.</span></span>
<span data-ttu-id="8e820-224">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8e820-224">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8e820-225">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8e820-225">Additional resources</span></span>

* [<span data-ttu-id="8e820-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e820-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="8e820-227">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8e820-227">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/youearnedit-tutorial/tutorial_general_01.png
[2]: ./media/youearnedit-tutorial/tutorial_general_02.png
[3]: ./media/youearnedit-tutorial/tutorial_general_03.png
[4]: ./media/youearnedit-tutorial/tutorial_general_04.png

[100]: ./media/youearnedit-tutorial/tutorial_general_100.png

[200]: ./media/youearnedit-tutorial/tutorial_general_200.png
[201]: ./media/youearnedit-tutorial/tutorial_general_201.png
[202]: ./media/youearnedit-tutorial/tutorial_general_202.png
[203]: ./media/youearnedit-tutorial/tutorial_general_203.png