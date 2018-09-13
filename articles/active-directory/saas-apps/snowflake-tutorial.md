---
title: 'Tutorial: Azure Active Directory integration with Snowflake | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Snowflake.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3488ac27-0417-4ad9-b9a3-08325fe8ea0d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2018
ms.author: jeedes
ms.openlocfilehash: 247d18eb13f7bad10cbfd89891a80d2d1c6135c3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968480"
---
# <a name="tutorial-azure-active-directory-integration-with-snowflake"></a><span data-ttu-id="3cac7-103">Tutorial: Azure Active Directory integration with Snowflake</span><span class="sxs-lookup"><span data-stu-id="3cac7-103">Tutorial: Azure Active Directory integration with Snowflake</span></span>

<span data-ttu-id="3cac7-104">In this tutorial, you learn how to integrate Snowflake with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3cac7-104">In this tutorial, you learn how to integrate Snowflake with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3cac7-105">Integrating Snowflake with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3cac7-105">Integrating Snowflake with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3cac7-106">You can control in Azure AD who has access to Snowflake.</span><span class="sxs-lookup"><span data-stu-id="3cac7-106">You can control in Azure AD who has access to Snowflake.</span></span>
- <span data-ttu-id="3cac7-107">You can enable your users to automatically get signed-on to Snowflake (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="3cac7-107">You can enable your users to automatically get signed-on to Snowflake (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3cac7-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3cac7-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="3cac7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="3cac7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cac7-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3cac7-110">Prerequisites</span></span>

<span data-ttu-id="3cac7-111">To configure Azure AD integration with Snowflake, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="3cac7-111">To configure Azure AD integration with Snowflake, you need the following items:</span></span>

- <span data-ttu-id="3cac7-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="3cac7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3cac7-113">A Snowflake single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="3cac7-113">A Snowflake single sign-on enabled subscription</span></span>
- <span data-ttu-id="3cac7-114">Customers who don't have a Snowflake account, and would like to try it out through Azure AD app gallery, please refer [this](https://trial.snowflake.net/?cloud=azure&utm_source=azure-marketplace&utm_medium=referral&utm_campaign=self-service-azure-mp) link.</span><span class="sxs-lookup"><span data-stu-id="3cac7-114">Customers who don't have a Snowflake account, and would like to try it out through Azure AD app gallery, please refer [this](https://trial.snowflake.net/?cloud=azure&utm_source=azure-marketplace&utm_medium=referral&utm_campaign=self-service-azure-mp) link.</span></span>

> [!NOTE]
> <span data-ttu-id="3cac7-115">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="3cac7-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3cac7-116">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="3cac7-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3cac7-117">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="3cac7-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3cac7-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3cac7-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3cac7-119">Scenario description</span><span class="sxs-lookup"><span data-stu-id="3cac7-119">Scenario description</span></span>
<span data-ttu-id="3cac7-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="3cac7-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3cac7-121">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="3cac7-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3cac7-122">Adding Snowflake from the gallery</span><span class="sxs-lookup"><span data-stu-id="3cac7-122">Adding Snowflake from the gallery</span></span>
2. <span data-ttu-id="3cac7-123">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3cac7-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-snowflake-from-the-gallery"></a><span data-ttu-id="3cac7-124">Adding Snowflake from the gallery</span><span class="sxs-lookup"><span data-stu-id="3cac7-124">Adding Snowflake from the gallery</span></span>
<span data-ttu-id="3cac7-125">To configure the integration of Snowflake into Azure AD, you need to add Snowflake from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="3cac7-125">To configure the integration of Snowflake into Azure AD, you need to add Snowflake from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3cac7-126">**To add Snowflake from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3cac7-126">**To add Snowflake from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3cac7-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="3cac7-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="3cac7-129">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="3cac7-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3cac7-130">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3cac7-130">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="3cac7-132">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="3cac7-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="3cac7-134">In the search box, type **Snowflake**, select **Snowflake** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="3cac7-134">In the search box, type **Snowflake**, select **Snowflake** from result panel then click **Add** button to add the application.</span></span>

    ![Snowflake in the results list](./media/snowflake-tutorial/tutorial_snowflake_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3cac7-136">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3cac7-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3cac7-137">In this section, you configure and test Azure AD single sign-on with Snowflake based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3cac7-137">In this section, you configure and test Azure AD single sign-on with Snowflake based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3cac7-138">For single sign-on to work, Azure AD needs to know what the counterpart user in Snowflake is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3cac7-138">For single sign-on to work, Azure AD needs to know what the counterpart user in Snowflake is to a user in Azure AD.</span></span> <span data-ttu-id="3cac7-139">In other words, a link relationship between an Azure AD user and the related user in Snowflake needs to be established.</span><span class="sxs-lookup"><span data-stu-id="3cac7-139">In other words, a link relationship between an Azure AD user and the related user in Snowflake needs to be established.</span></span>

<span data-ttu-id="3cac7-140">To configure and test Azure AD single sign-on with Snowflake, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="3cac7-140">To configure and test Azure AD single sign-on with Snowflake, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3cac7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="3cac7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3cac7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3cac7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3cac7-143">**[Create a Snowflake test user](#create-a-snowflake-test-user)** - to have a counterpart of Britta Simon in Snowflake that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="3cac7-143">**[Create a Snowflake test user](#create-a-snowflake-test-user)** - to have a counterpart of Britta Simon in Snowflake that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3cac7-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3cac7-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3cac7-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="3cac7-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3cac7-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3cac7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3cac7-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Snowflake application.</span><span class="sxs-lookup"><span data-stu-id="3cac7-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Snowflake application.</span></span>

<span data-ttu-id="3cac7-148">**To configure Azure AD single sign-on with Snowflake, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3cac7-148">**To configure Azure AD single sign-on with Snowflake, perform the following steps:**</span></span>

1. <span data-ttu-id="3cac7-149">In the Azure portal, on the **Snowflake** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3cac7-149">In the Azure portal, on the **Snowflake** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="3cac7-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3cac7-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/snowflake-tutorial/tutorial_snowflake_samlbase.png)

3. <span data-ttu-id="3cac7-153">On the **Snowflake Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3cac7-153">On the **Snowflake Domain and URLs** section, perform the following steps:</span></span>

    ![Snowflake Domain and URLs single sign-on information](./media/snowflake-tutorial/tutorial_snowflake_url.png)

    <span data-ttu-id="3cac7-155">a.</span><span class="sxs-lookup"><span data-stu-id="3cac7-155">a.</span></span> <span data-ttu-id="3cac7-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<SNOWFLAKE-URL>.snowflakecomputing.com`</span><span class="sxs-lookup"><span data-stu-id="3cac7-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<SNOWFLAKE-URL>.snowflakecomputing.com`</span></span>

    <span data-ttu-id="3cac7-157">b.</span><span class="sxs-lookup"><span data-stu-id="3cac7-157">b.</span></span> <span data-ttu-id="3cac7-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<SNOWFLAKE-URL>.snowflakecomputing.com/fed/login`</span><span class="sxs-lookup"><span data-stu-id="3cac7-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<SNOWFLAKE-URL>.snowflakecomputing.com/fed/login`</span></span>

4. <span data-ttu-id="3cac7-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="3cac7-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Snowflake Domain and URLs single sign-on information](./media/snowflake-tutorial/tutorial_snowflake_url1.png)

    <span data-ttu-id="3cac7-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<SNOWFLAKE-URL>.snowflakecomputing.com`</span><span class="sxs-lookup"><span data-stu-id="3cac7-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<SNOWFLAKE-URL>.snowflakecomputing.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="3cac7-162">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="3cac7-162">These values are not real.</span></span> <span data-ttu-id="3cac7-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="3cac7-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span>

5. <span data-ttu-id="3cac7-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="3cac7-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/snowflake-tutorial/tutorial_snowflake_certificate.png) 

6. <span data-ttu-id="3cac7-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="3cac7-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/snowflake-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="3cac7-168">On the **Snowflake Configuration** section, click **Configure Snowflake** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="3cac7-168">On the **Snowflake Configuration** section, click **Configure Snowflake** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3cac7-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="3cac7-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Snowflake Configuration](./media/snowflake-tutorial/tutorial_snowflake_configure.png) 

8. <span data-ttu-id="3cac7-171">In a different web browser window, login to Snowflake as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="3cac7-171">In a different web browser window, login to Snowflake as a Security Administrator.</span></span>

9. <span data-ttu-id="3cac7-172">Run the below SQL query on worksheet by setting the **certificate** value to the **dowloaded certificate** and **ssoUrl** to the copied **SAML Single Sign-On Service URL** from Azure AD to the value as shown below.</span><span class="sxs-lookup"><span data-stu-id="3cac7-172">Run the below SQL query on worksheet by setting the **certificate** value to the **dowloaded certificate** and **ssoUrl** to the copied **SAML Single Sign-On Service URL** from Azure AD to the value as shown below.</span></span>

    ![Snowflake sql](./media/snowflake-tutorial/tutorial_snowflake_sql.png) 

    ```
    use role accountadmin;
    alter account set saml_identity_provider = '{
    "certificate": "<Paste the content of downloaded certificate from Azure portal>",
    "ssoUrl":"<SAML single sign-on service URL value which you have copied from the Azure portal>",
    "type":"custom",
    "label":"AzureAD"
    }';
    alter account set sso_login_page = TRUE;
    ```

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3cac7-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3cac7-174">Create an Azure AD test user</span></span>

<span data-ttu-id="3cac7-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3cac7-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="3cac7-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3cac7-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3cac7-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="3cac7-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/snowflake-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3cac7-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="3cac7-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/snowflake-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3cac7-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="3cac7-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/snowflake-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3cac7-184">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3cac7-184">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/snowflake-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3cac7-186">a.</span><span class="sxs-lookup"><span data-stu-id="3cac7-186">a.</span></span> <span data-ttu-id="3cac7-187">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3cac7-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3cac7-188">b.</span><span class="sxs-lookup"><span data-stu-id="3cac7-188">b.</span></span> <span data-ttu-id="3cac7-189">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3cac7-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="3cac7-190">c.</span><span class="sxs-lookup"><span data-stu-id="3cac7-190">c.</span></span> <span data-ttu-id="3cac7-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="3cac7-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="3cac7-192">d.</span><span class="sxs-lookup"><span data-stu-id="3cac7-192">d.</span></span> <span data-ttu-id="3cac7-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3cac7-193">Click **Create**.</span></span>
 
### <a name="create-a-snowflake-test-user"></a><span data-ttu-id="3cac7-194">Create a Snowflake test user</span><span class="sxs-lookup"><span data-stu-id="3cac7-194">Create a Snowflake test user</span></span>

<span data-ttu-id="3cac7-195">To enable Azure AD users to log in to Snowflake, they must be provisioned into Snowflake.</span><span class="sxs-lookup"><span data-stu-id="3cac7-195">To enable Azure AD users to log in to Snowflake, they must be provisioned into Snowflake.</span></span> <span data-ttu-id="3cac7-196">In Snowflake, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="3cac7-196">In Snowflake, provisioning is a manual task.</span></span>

<span data-ttu-id="3cac7-197">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3cac7-197">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="3cac7-198">Log in to Snowflake as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="3cac7-198">Log in to Snowflake as a Security Administrator.</span></span>

2. <span data-ttu-id="3cac7-199">**Switch Role** to **ACCOUNTADMIN**, by clicking on **profile** on the top right side of page.</span><span class="sxs-lookup"><span data-stu-id="3cac7-199">**Switch Role** to **ACCOUNTADMIN**, by clicking on **profile** on the top right side of page.</span></span>  

    ![<span data-ttu-id="3cac7-200">The Snowflake admin</span><span class="sxs-lookup"><span data-stu-id="3cac7-200">The Snowflake admin</span></span> ](./media/snowflake-tutorial/tutorial_snowflake_accountadmin.png)

3. <span data-ttu-id="3cac7-201">Create the user by running the below SQL query, ensuring "Login name" is set to the Azure AD username on the worksheet as shown below.</span><span class="sxs-lookup"><span data-stu-id="3cac7-201">Create the user by running the below SQL query, ensuring "Login name" is set to the Azure AD username on the worksheet as shown below.</span></span>

    ![<span data-ttu-id="3cac7-202">The Snowflake adminsql</span><span class="sxs-lookup"><span data-stu-id="3cac7-202">The Snowflake adminsql</span></span> ](./media/snowflake-tutorial/tutorial_snowflake_usersql.png)

    ```

    use role accountadmin;
    CREATE USER britta_simon PASSWORD = '' LOGIN_NAME = 'BrittaSimon@contoso.com' DISPLAY_NAME = 'Britta Simon';
    ```

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3cac7-203">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3cac7-203">Assign the Azure AD test user</span></span>

<span data-ttu-id="3cac7-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Snowflake.</span><span class="sxs-lookup"><span data-stu-id="3cac7-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Snowflake.</span></span>

![Assign the user role][200] 

<span data-ttu-id="3cac7-206">**To assign Britta Simon to Snowflake, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3cac7-206">**To assign Britta Simon to Snowflake, perform the following steps:**</span></span>

1. <span data-ttu-id="3cac7-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="3cac7-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="3cac7-209">In the applications list, select **Snowflake**.</span><span class="sxs-lookup"><span data-stu-id="3cac7-209">In the applications list, select **Snowflake**.</span></span>

    ![The Snowflake link in the Applications list](./media/snowflake-tutorial/tutorial_snowflake_app.png)  

3. <span data-ttu-id="3cac7-211">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="3cac7-211">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="3cac7-213">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="3cac7-213">Click **Add** button.</span></span> <span data-ttu-id="3cac7-214">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3cac7-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="3cac7-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="3cac7-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3cac7-217">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="3cac7-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3cac7-218">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="3cac7-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3cac7-219">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="3cac7-219">Test single sign-on</span></span>

<span data-ttu-id="3cac7-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3cac7-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3cac7-221">When you click the Snowflake tile in the Access Panel, you should get automatically signed-on to your Snowflake application.</span><span class="sxs-lookup"><span data-stu-id="3cac7-221">When you click the Snowflake tile in the Access Panel, you should get automatically signed-on to your Snowflake application.</span></span>
<span data-ttu-id="3cac7-222">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3cac7-222">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3cac7-223">Additional resources</span><span class="sxs-lookup"><span data-stu-id="3cac7-223">Additional resources</span></span>

* [<span data-ttu-id="3cac7-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3cac7-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="3cac7-225">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3cac7-225">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/snowflake-tutorial/tutorial_general_01.png
[2]: ./media/snowflake-tutorial/tutorial_general_02.png
[3]: ./media/snowflake-tutorial/tutorial_general_03.png
[4]: ./media/snowflake-tutorial/tutorial_general_04.png

[100]: ./media/snowflake-tutorial/tutorial_general_100.png

[200]: ./media/snowflake-tutorial/tutorial_general_200.png
[201]: ./media/snowflake-tutorial/tutorial_general_201.png
[202]: ./media/snowflake-tutorial/tutorial_general_202.png
[203]: ./media/snowflake-tutorial/tutorial_general_203.png

