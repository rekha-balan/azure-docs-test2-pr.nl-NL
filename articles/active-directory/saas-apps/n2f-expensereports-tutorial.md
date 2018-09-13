---
title: 'Tutorial: Azure Active Directory integration with N2F - Expense reports | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and N2F - Expense reports.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f56d53d7-5a08-490a-bfb9-78fefc2751ec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2018
ms.author: jeedes
ms.openlocfilehash: 27fb299bc3bbbbf75bdf40ae02eac627763ce6d4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868862"
---
# <a name="tutorial-azure-active-directory-integration-with-n2f---expense-reports"></a><span data-ttu-id="7f214-103">Tutorial: Azure Active Directory integration with N2F - Expense reports</span><span class="sxs-lookup"><span data-stu-id="7f214-103">Tutorial: Azure Active Directory integration with N2F - Expense reports</span></span>

<span data-ttu-id="7f214-104">In this tutorial, you learn how to integrate N2F - Expense reports with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7f214-104">In this tutorial, you learn how to integrate N2F - Expense reports with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7f214-105">Integrating N2F - Expense reports with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7f214-105">Integrating N2F - Expense reports with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7f214-106">You can control in Azure AD who has access to N2F - Expense reports.</span><span class="sxs-lookup"><span data-stu-id="7f214-106">You can control in Azure AD who has access to N2F - Expense reports.</span></span>
- <span data-ttu-id="7f214-107">You can enable your users to automatically get signed-on to N2F - Expense reports (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="7f214-107">You can enable your users to automatically get signed-on to N2F - Expense reports (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7f214-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7f214-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="7f214-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span><span class="sxs-lookup"><span data-stu-id="7f214-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f214-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7f214-110">Prerequisites</span></span>

<span data-ttu-id="7f214-111">To configure Azure AD integration with N2F - Expense reports, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7f214-111">To configure Azure AD integration with N2F - Expense reports, you need the following items:</span></span>

- <span data-ttu-id="7f214-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7f214-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7f214-113">A N2F - Expense reports single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7f214-113">A N2F - Expense reports single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7f214-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7f214-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7f214-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7f214-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7f214-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="7f214-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7f214-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7f214-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7f214-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7f214-118">Scenario description</span></span>

<span data-ttu-id="7f214-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7f214-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7f214-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7f214-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7f214-121">Adding N2F - Expense reports from the gallery</span><span class="sxs-lookup"><span data-stu-id="7f214-121">Adding N2F - Expense reports from the gallery</span></span>
2. <span data-ttu-id="7f214-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7f214-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-n2f---expense-reports-from-the-gallery"></a><span data-ttu-id="7f214-123">Adding N2F - Expense reports from the gallery</span><span class="sxs-lookup"><span data-stu-id="7f214-123">Adding N2F - Expense reports from the gallery</span></span>

<span data-ttu-id="7f214-124">To configure the integration of N2F - Expense reports into Azure AD, you need to add N2F - Expense reports from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7f214-124">To configure the integration of N2F - Expense reports into Azure AD, you need to add N2F - Expense reports from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7f214-125">**To add N2F - Expense reports from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7f214-125">**To add N2F - Expense reports from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7f214-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7f214-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="7f214-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="7f214-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7f214-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7f214-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="7f214-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="7f214-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="7f214-133">In the search box, type **N2F - Expense reports**, select **N2F - Expense reports** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="7f214-133">In the search box, type **N2F - Expense reports**, select **N2F - Expense reports** from result panel then click **Add** button to add the application.</span></span>

    ![N2F - Expense reports in the results list](./media/n2f-expensereports-tutorial/tutorial_n2f-expensereports_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7f214-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7f214-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7f214-136">In this section, you configure and test Azure AD single sign-on with N2F - Expense reports based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7f214-136">In this section, you configure and test Azure AD single sign-on with N2F - Expense reports based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7f214-137">For single sign-on to work, Azure AD needs to know what the counterpart user in N2F - Expense reports is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f214-137">For single sign-on to work, Azure AD needs to know what the counterpart user in N2F - Expense reports is to a user in Azure AD.</span></span> <span data-ttu-id="7f214-138">In other words, a link relationship between an Azure AD user and the related user in N2F - Expense reports needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7f214-138">In other words, a link relationship between an Azure AD user and the related user in N2F - Expense reports needs to be established.</span></span>

<span data-ttu-id="7f214-139">To configure and test Azure AD single sign-on with N2F - Expense reports, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7f214-139">To configure and test Azure AD single sign-on with N2F - Expense reports, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7f214-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7f214-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7f214-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f214-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7f214-142">**[Create a N2F - Expense reports test user](#create-a-n2f---expense-reports-test-use)** - to have a counterpart of Britta Simon in N2F - Expense reports that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="7f214-142">**[Create a N2F - Expense reports test user](#create-a-n2f---expense-reports-test-use)** - to have a counterpart of Britta Simon in N2F - Expense reports that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7f214-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7f214-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7f214-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7f214-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7f214-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7f214-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7f214-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your N2F - Expense reports application.</span><span class="sxs-lookup"><span data-stu-id="7f214-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your N2F - Expense reports application.</span></span>

<span data-ttu-id="7f214-147">**To configure Azure AD single sign-on with N2F - Expense reports, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7f214-147">**To configure Azure AD single sign-on with N2F - Expense reports, perform the following steps:**</span></span>

1. <span data-ttu-id="7f214-148">In the Azure portal, on the **N2F - Expense reports** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7f214-148">In the Azure portal, on the **N2F - Expense reports** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="7f214-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7f214-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/n2f-expensereports-tutorial/tutorial_n2f-expensereports_samlbase.png)

3. <span data-ttu-id="7f214-152">On the **N2F - Expense reports Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span><span class="sxs-lookup"><span data-stu-id="7f214-152">On the **N2F - Expense reports Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![N2F - Expense reports Domain and URLs single sign-on information](./media/n2f-expensereports-tutorial/tutorial_n2f-expensereports_url1.png)

4. <span data-ttu-id="7f214-154">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="7f214-154">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![N2F - Expense reports Domain and URLs single sign-on information](./media/n2f-expensereports-tutorial/tutorial_n2f-expensereports_url2.png)

    <span data-ttu-id="7f214-156">In the **Sign-on URL** textbox, type the URL: `https://www.n2f.com/app/`</span><span class="sxs-lookup"><span data-stu-id="7f214-156">In the **Sign-on URL** textbox, type the URL: `https://www.n2f.com/app/`</span></span>

5. <span data-ttu-id="7f214-157">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into Notepad.</span><span class="sxs-lookup"><span data-stu-id="7f214-157">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into Notepad.</span></span>

    ![The Certificate download link](./media/n2f-expensereports-tutorial/tutorial_n2f-expensereports_certificate.png)

6. <span data-ttu-id="7f214-159">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7f214-159">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/n2f-expensereports-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="7f214-161">On the **N2F - Expense reports Configuration** section, click **Configure N2F - Expense reports** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="7f214-161">On the **N2F - Expense reports Configuration** section, click **Configure N2F - Expense reports** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7f214-162">Copy the **SAML Entity ID** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="7f214-162">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![N2F - Expense reports Configuration](./media/n2f-expensereports-tutorial/tutorial_n2f-expensereports_configure.png)

8. <span data-ttu-id="7f214-164">In a different web browser window, sign in to your N2F - Expense reports company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7f214-164">In a different web browser window, sign in to your N2F - Expense reports company site as an administrator.</span></span>

9. <span data-ttu-id="7f214-165">Click on **Settings** and then select **Advance Settings** from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="7f214-165">Click on **Settings** and then select **Advance Settings** from the dropdown.</span></span>

    ![N2F - Expense reports Configuration](./media/n2f-expensereports-tutorial/configure1.png)

10. <span data-ttu-id="7f214-167">Select **Account settings** tab.</span><span class="sxs-lookup"><span data-stu-id="7f214-167">Select **Account settings** tab.</span></span>

    ![N2F - Expense reports Configuration](./media/n2f-expensereports-tutorial/configure2.png)

11. <span data-ttu-id="7f214-169">Select **Authentication** and then select **+ Add an authentication method** tab.</span><span class="sxs-lookup"><span data-stu-id="7f214-169">Select **Authentication** and then select **+ Add an authentication method** tab.</span></span>

    ![N2F - Expense reports Configuration](./media/n2f-expensereports-tutorial/configure3.png)

12. <span data-ttu-id="7f214-171">Select **SAML Microsoft Office 365** as Authentication method.</span><span class="sxs-lookup"><span data-stu-id="7f214-171">Select **SAML Microsoft Office 365** as Authentication method.</span></span>

    ![N2F - Expense reports Configuration](./media/n2f-expensereports-tutorial/configure4.png)

13. <span data-ttu-id="7f214-173">On the **Authentication method** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7f214-173">On the **Authentication method** section, perform the following steps:</span></span>

    ![N2F - Expense reports Configuration](./media/n2f-expensereports-tutorial/configure5.png)

    <span data-ttu-id="7f214-175">a.</span><span class="sxs-lookup"><span data-stu-id="7f214-175">a.</span></span> <span data-ttu-id="7f214-176">In the **Entity ID** textbox, paste the **SAML Entity ID** value, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7f214-176">In the **Entity ID** textbox, paste the **SAML Entity ID** value, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="7f214-177">b.</span><span class="sxs-lookup"><span data-stu-id="7f214-177">b.</span></span> <span data-ttu-id="7f214-178">In the **Metadata URL** textbox, paste the **App Federation Metadata Url** value, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7f214-178">In the **Metadata URL** textbox, paste the **App Federation Metadata Url** value, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="7f214-179">c.</span><span class="sxs-lookup"><span data-stu-id="7f214-179">c.</span></span> <span data-ttu-id="7f214-180">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="7f214-180">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7f214-181">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7f214-181">Create an Azure AD test user</span></span>

<span data-ttu-id="7f214-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f214-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="7f214-184">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7f214-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7f214-185">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="7f214-185">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/n2f-expensereports-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7f214-187">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="7f214-187">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/n2f-expensereports-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7f214-189">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="7f214-189">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/n2f-expensereports-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7f214-191">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7f214-191">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/n2f-expensereports-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7f214-193">a.</span><span class="sxs-lookup"><span data-stu-id="7f214-193">a.</span></span> <span data-ttu-id="7f214-194">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7f214-194">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7f214-195">b.</span><span class="sxs-lookup"><span data-stu-id="7f214-195">b.</span></span> <span data-ttu-id="7f214-196">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f214-196">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="7f214-197">c.</span><span class="sxs-lookup"><span data-stu-id="7f214-197">c.</span></span> <span data-ttu-id="7f214-198">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="7f214-198">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="7f214-199">d.</span><span class="sxs-lookup"><span data-stu-id="7f214-199">d.</span></span> <span data-ttu-id="7f214-200">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7f214-200">Click **Create**.</span></span>

### <a name="create-a-n2f---expense-reports-test-user"></a><span data-ttu-id="7f214-201">Create a N2F - Expense reports test user</span><span class="sxs-lookup"><span data-stu-id="7f214-201">Create a N2F - Expense reports test user</span></span>

<span data-ttu-id="7f214-202">To enable Azure AD users to log in to N2F - Expense reports, they must be provisioned into N2F - Expense reports.</span><span class="sxs-lookup"><span data-stu-id="7f214-202">To enable Azure AD users to log in to N2F - Expense reports, they must be provisioned into N2F - Expense reports.</span></span> <span data-ttu-id="7f214-203">In the case of N2F - Expense reports, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="7f214-203">In the case of N2F - Expense reports, provisioning is a manual task.</span></span>

<span data-ttu-id="7f214-204">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7f214-204">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="7f214-205">Log in to your N2F - Expense reports company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7f214-205">Log in to your N2F - Expense reports company site as an administrator.</span></span>

2. <span data-ttu-id="7f214-206">Click on **Settings** and then select **Advance Settings** from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="7f214-206">Click on **Settings** and then select **Advance Settings** from the dropdown.</span></span>

   ![N2F - Expense Add user](./media/n2f-expensereports-tutorial/configure1.png)

3. <span data-ttu-id="7f214-208">Select **Users** tab from left navigation panel.</span><span class="sxs-lookup"><span data-stu-id="7f214-208">Select **Users** tab from left navigation panel.</span></span>

    ![N2F - Expense reports Configuration](./media/n2f-expensereports-tutorial/user1.png)

4. <span data-ttu-id="7f214-210">Select **+ New user** tab.</span><span class="sxs-lookup"><span data-stu-id="7f214-210">Select **+ New user** tab.</span></span>

   ![N2F - Expense reports Configuration](./media/n2f-expensereports-tutorial/user2.png)

5. <span data-ttu-id="7f214-212">On the **User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7f214-212">On the **User** section, perform the following steps:</span></span>

    ![N2F - Expense reports Configuration](./media/n2f-expensereports-tutorial/user3.png)

    <span data-ttu-id="7f214-214">a.</span><span class="sxs-lookup"><span data-stu-id="7f214-214">a.</span></span> <span data-ttu-id="7f214-215">In the **Email address** textbox, enter the email address of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="7f214-215">In the **Email address** textbox, enter the email address of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="7f214-216">b.</span><span class="sxs-lookup"><span data-stu-id="7f214-216">b.</span></span> <span data-ttu-id="7f214-217">In the **First name** textbox, enter the first name of user like **Britta**.</span><span class="sxs-lookup"><span data-stu-id="7f214-217">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="7f214-218">c.</span><span class="sxs-lookup"><span data-stu-id="7f214-218">c.</span></span> <span data-ttu-id="7f214-219">In the **Name** textbox, enter the name of user like **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7f214-219">In the **Name** textbox, enter the name of user like **BrittaSimon**.</span></span>

    <span data-ttu-id="7f214-220">d.</span><span class="sxs-lookup"><span data-stu-id="7f214-220">d.</span></span> <span data-ttu-id="7f214-221">Choose **Role, Direct manager (N+1)**, and **Division** as per your organization requirement.</span><span class="sxs-lookup"><span data-stu-id="7f214-221">Choose **Role, Direct manager (N+1)**, and **Division** as per your organization requirement.</span></span>

    <span data-ttu-id="7f214-222">e.</span><span class="sxs-lookup"><span data-stu-id="7f214-222">e.</span></span> <span data-ttu-id="7f214-223">Click **Validate and send invitation**.</span><span class="sxs-lookup"><span data-stu-id="7f214-223">Click **Validate and send invitation**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7f214-224">If you are facing any problems while adding the user, please contact [N2F - Expense reports support team](mailto:support@n2f.com)</span><span class="sxs-lookup"><span data-stu-id="7f214-224">If you are facing any problems while adding the user, please contact [N2F - Expense reports support team](mailto:support@n2f.com)</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7f214-225">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7f214-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="7f214-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to N2F - Expense reports.</span><span class="sxs-lookup"><span data-stu-id="7f214-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to N2F - Expense reports.</span></span>

![Assign the user role][200]

<span data-ttu-id="7f214-228">**To assign Britta Simon to N2F - Expense reports, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7f214-228">**To assign Britta Simon to N2F - Expense reports, perform the following steps:**</span></span>

1. <span data-ttu-id="7f214-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7f214-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="7f214-231">In the applications list, select **N2F - Expense reports**.</span><span class="sxs-lookup"><span data-stu-id="7f214-231">In the applications list, select **N2F - Expense reports**.</span></span>

    ![The N2F - Expense reports link in the Applications list](./media/n2f-expensereports-tutorial/tutorial_n2f-expensereports_app.png)  

3. <span data-ttu-id="7f214-233">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="7f214-233">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="7f214-235">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="7f214-235">Click **Add** button.</span></span> <span data-ttu-id="7f214-236">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7f214-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="7f214-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="7f214-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7f214-239">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="7f214-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7f214-240">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7f214-240">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="7f214-241">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="7f214-241">Test single sign-on</span></span>

<span data-ttu-id="7f214-242">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7f214-242">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7f214-243">When you click the N2F - Expense reports tile in the Access Panel, you should get automatically signed-on to your N2F - Expense reports application.</span><span class="sxs-lookup"><span data-stu-id="7f214-243">When you click the N2F - Expense reports tile in the Access Panel, you should get automatically signed-on to your N2F - Expense reports application.</span></span>
<span data-ttu-id="7f214-244">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7f214-244">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7f214-245">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7f214-245">Additional resources</span></span>

* [<span data-ttu-id="7f214-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f214-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="7f214-247">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7f214-247">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/n2f-expensereports-tutorial/tutorial_general_01.png
[2]: ./media/n2f-expensereports-tutorial/tutorial_general_02.png
[3]: ./media/n2f-expensereports-tutorial/tutorial_general_03.png
[4]: ./media/n2f-expensereports-tutorial/tutorial_general_04.png

[100]: ./media/n2f-expensereports-tutorial/tutorial_general_100.png

[200]: ./media/n2f-expensereports-tutorial/tutorial_general_200.png
[201]: ./media/n2f-expensereports-tutorial/tutorial_general_201.png
[202]: ./media/n2f-expensereports-tutorial/tutorial_general_202.png
[203]: ./media/n2f-expensereports-tutorial/tutorial_general_203.png

