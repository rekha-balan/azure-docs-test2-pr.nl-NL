---
title: 'Tutorial: Azure Active Directory integration with JDA Cloud | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and JDA Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 06af825f-79ec-4de9-8851-c79d65d1e586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/31/2018
ms.author: jeedes
ms.openlocfilehash: 371ff15121e3da0bec5be6159fea9c6764b0aeda
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865069"
---
# <a name="tutorial-azure-active-directory-integration-with-jda-cloud"></a><span data-ttu-id="f1854-103">Tutorial: Azure Active Directory integration with JDA Cloud</span><span class="sxs-lookup"><span data-stu-id="f1854-103">Tutorial: Azure Active Directory integration with JDA Cloud</span></span>

<span data-ttu-id="f1854-104">In this tutorial, you learn how to integrate JDA Cloud with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f1854-104">In this tutorial, you learn how to integrate JDA Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1854-105">Integrating JDA Cloud with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f1854-105">Integrating JDA Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f1854-106">You can control in Azure AD who has access to JDA Cloud.</span><span class="sxs-lookup"><span data-stu-id="f1854-106">You can control in Azure AD who has access to JDA Cloud.</span></span>
- <span data-ttu-id="f1854-107">You can enable your users to automatically get signed-on to JDA Cloud (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="f1854-107">You can enable your users to automatically get signed-on to JDA Cloud (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f1854-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f1854-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f1854-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span><span class="sxs-lookup"><span data-stu-id="f1854-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1854-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f1854-110">Prerequisites</span></span>

<span data-ttu-id="f1854-111">To configure Azure AD integration with JDA Cloud, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f1854-111">To configure Azure AD integration with JDA Cloud, you need the following items:</span></span>

- <span data-ttu-id="f1854-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f1854-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1854-113">A JDA Cloud single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f1854-113">A JDA Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f1854-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f1854-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f1854-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f1854-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1854-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="f1854-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f1854-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1854-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f1854-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f1854-118">Scenario description</span></span>

<span data-ttu-id="f1854-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f1854-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1854-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f1854-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1854-121">Adding JDA Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="f1854-121">Adding JDA Cloud from the gallery</span></span>
2. <span data-ttu-id="f1854-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f1854-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jda-cloud-from-the-gallery"></a><span data-ttu-id="f1854-123">Adding JDA Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="f1854-123">Adding JDA Cloud from the gallery</span></span>

<span data-ttu-id="f1854-124">To configure the integration of JDA Cloud into Azure AD, you need to add JDA Cloud from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f1854-124">To configure the integration of JDA Cloud into Azure AD, you need to add JDA Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f1854-125">**To add JDA Cloud from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f1854-125">**To add JDA Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f1854-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f1854-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="f1854-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="f1854-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f1854-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f1854-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="f1854-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="f1854-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="f1854-133">In the search box, type **JDA Cloud**, select **JDA Cloud** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="f1854-133">In the search box, type **JDA Cloud**, select **JDA Cloud** from result panel then click **Add** button to add the application.</span></span>

    ![JDA Cloud in the results list](./media/jdacloud-tutorial/tutorial_jdacloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f1854-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f1854-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f1854-136">In this section, you configure and test Azure AD single sign-on with JDA Cloud based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f1854-136">In this section, you configure and test Azure AD single sign-on with JDA Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f1854-137">For single sign-on to work, Azure AD needs to know what the counterpart user in JDA Cloud is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1854-137">For single sign-on to work, Azure AD needs to know what the counterpart user in JDA Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="f1854-138">In other words, a link relationship between an Azure AD user and the related user in JDA Cloud needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f1854-138">In other words, a link relationship between an Azure AD user and the related user in JDA Cloud needs to be established.</span></span>

<span data-ttu-id="f1854-139">To configure and test Azure AD single sign-on with JDA Cloud, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f1854-139">To configure and test Azure AD single sign-on with JDA Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f1854-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f1854-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f1854-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1854-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1854-142">**[Create a JDA Cloud test user](#create-a-jda-cloud-test-user)** - to have a counterpart of Britta Simon in JDA Cloud that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="f1854-142">**[Create a JDA Cloud test user](#create-a-jda-cloud-test-user)** - to have a counterpart of Britta Simon in JDA Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f1854-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f1854-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1854-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f1854-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f1854-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f1854-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f1854-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JDA Cloud application.</span><span class="sxs-lookup"><span data-stu-id="f1854-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JDA Cloud application.</span></span>

<span data-ttu-id="f1854-147">**To configure Azure AD single sign-on with JDA Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f1854-147">**To configure Azure AD single sign-on with JDA Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="f1854-148">In the Azure portal, on the **JDA Cloud** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f1854-148">In the Azure portal, on the **JDA Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="f1854-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f1854-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/jdacloud-tutorial/tutorial_jdacloud_samlbase.png)

3. <span data-ttu-id="f1854-152">On the **JDA Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="f1854-152">On the **JDA Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![JDA Cloud Domain and URLs single sign-on information](./media/jdacloud-tutorial/tutorial_jdacloud_url1.png)

    <span data-ttu-id="f1854-154">a.</span><span class="sxs-lookup"><span data-stu-id="f1854-154">a.</span></span> <span data-ttu-id="f1854-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.jdadelivers.com`</span><span class="sxs-lookup"><span data-stu-id="f1854-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.jdadelivers.com`</span></span>

    <span data-ttu-id="f1854-156">b.</span><span class="sxs-lookup"><span data-stu-id="f1854-156">b.</span></span> <span data-ttu-id="f1854-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.jdadelivers.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="f1854-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.jdadelivers.com/sp/ACS.saml2`</span></span>

4. <span data-ttu-id="f1854-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="f1854-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![JDA Cloud Domain and URLs single sign-on information](./media/jdacloud-tutorial/tutorial_jdacloud_url2.png)

    <span data-ttu-id="f1854-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://ssonp-dl2.jdadelivers.com/sp/startSSO.ping?PartnerIdpId=<SAML Entity ID>`</span><span class="sxs-lookup"><span data-stu-id="f1854-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://ssonp-dl2.jdadelivers.com/sp/startSSO.ping?PartnerIdpId=<SAML Entity ID>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="f1854-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="f1854-161">These values are not real.</span></span> <span data-ttu-id="f1854-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="f1854-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="f1854-163">You will get the **SAML Entity ID** value from the **Quick Reference section** in the **JDA Cloud Configuration** section.</span><span class="sxs-lookup"><span data-stu-id="f1854-163">You will get the **SAML Entity ID** value from the **Quick Reference section** in the **JDA Cloud Configuration** section.</span></span> <span data-ttu-id="f1854-164">Contact [JDA Cloud Client support team](https://support.jda.com/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="f1854-164">Contact [JDA Cloud Client support team](https://support.jda.com/) to get these values.</span></span>

5. <span data-ttu-id="f1854-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="f1854-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/jdacloud-tutorial/tutorial_jdacloud_certificate.png) 

6. <span data-ttu-id="f1854-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="f1854-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/jdacloud-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f1854-169">On the **JDA Cloud Configuration** section, click **Configure JDA Cloud** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="f1854-169">On the **JDA Cloud Configuration** section, click **Configure JDA Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f1854-170">Copy the **SAML Entity ID** from the **Quick Reference section**.</span><span class="sxs-lookup"><span data-stu-id="f1854-170">Copy the **SAML Entity ID** from the **Quick Reference section**.</span></span>

    ![Configure Single Sign-On](./media/jdacloud-tutorial/tutorial_jdacloud_configure.png)

8. <span data-ttu-id="f1854-172">To configure single sign-on on **JDA Cloud** side, you need to send the downloaded **Metadata XML** to [JDA Cloud support team](https://support.jda.com/).</span><span class="sxs-lookup"><span data-stu-id="f1854-172">To configure single sign-on on **JDA Cloud** side, you need to send the downloaded **Metadata XML** to [JDA Cloud support team](https://support.jda.com/).</span></span> <span data-ttu-id="f1854-173">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="f1854-173">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f1854-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f1854-174">Create an Azure AD test user</span></span>

<span data-ttu-id="f1854-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1854-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="f1854-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f1854-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f1854-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="f1854-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/jdacloud-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f1854-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="f1854-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/jdacloud-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f1854-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="f1854-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/jdacloud-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f1854-184">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f1854-184">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/jdacloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f1854-186">a.</span><span class="sxs-lookup"><span data-stu-id="f1854-186">a.</span></span> <span data-ttu-id="f1854-187">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f1854-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1854-188">b.</span><span class="sxs-lookup"><span data-stu-id="f1854-188">b.</span></span> <span data-ttu-id="f1854-189">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f1854-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f1854-190">c.</span><span class="sxs-lookup"><span data-stu-id="f1854-190">c.</span></span> <span data-ttu-id="f1854-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="f1854-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f1854-192">d.</span><span class="sxs-lookup"><span data-stu-id="f1854-192">d.</span></span> <span data-ttu-id="f1854-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f1854-193">Click **Create**.</span></span>

### <a name="create-a-jda-cloud-test-user"></a><span data-ttu-id="f1854-194">Create a JDA Cloud test user</span><span class="sxs-lookup"><span data-stu-id="f1854-194">Create a JDA Cloud test user</span></span>

<span data-ttu-id="f1854-195">In this section, you create a user called Britta Simon in JDA Cloud.</span><span class="sxs-lookup"><span data-stu-id="f1854-195">In this section, you create a user called Britta Simon in JDA Cloud.</span></span> <span data-ttu-id="f1854-196">Work with [JDA Cloud support team](https://support.jda.com/) to add the users in the JDA Cloud platform.</span><span class="sxs-lookup"><span data-stu-id="f1854-196">Work with [JDA Cloud support team](https://support.jda.com/) to add the users in the JDA Cloud platform.</span></span> <span data-ttu-id="f1854-197">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f1854-197">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f1854-198">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f1854-198">Assign the Azure AD test user</span></span>

<span data-ttu-id="f1854-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JDA Cloud.</span><span class="sxs-lookup"><span data-stu-id="f1854-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JDA Cloud.</span></span>

![Assign the user role][200] 

<span data-ttu-id="f1854-201">**To assign Britta Simon to JDA Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f1854-201">**To assign Britta Simon to JDA Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="f1854-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f1854-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="f1854-204">In the applications list, select **JDA Cloud**.</span><span class="sxs-lookup"><span data-stu-id="f1854-204">In the applications list, select **JDA Cloud**.</span></span>

    ![The JDA Cloud link in the Applications list](./media/jdacloud-tutorial/tutorial_jdacloud_app.png)  

3. <span data-ttu-id="f1854-206">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f1854-206">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="f1854-208">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="f1854-208">Click **Add** button.</span></span> <span data-ttu-id="f1854-209">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f1854-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="f1854-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="f1854-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f1854-212">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="f1854-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f1854-213">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f1854-213">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="f1854-214">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="f1854-214">Test single sign-on</span></span>

<span data-ttu-id="f1854-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f1854-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f1854-216">When you click the JDA Cloud tile in the Access Panel, you should get automatically signed-on to your JDA Cloud application.</span><span class="sxs-lookup"><span data-stu-id="f1854-216">When you click the JDA Cloud tile in the Access Panel, you should get automatically signed-on to your JDA Cloud application.</span></span>
<span data-ttu-id="f1854-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f1854-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f1854-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f1854-218">Additional resources</span></span>

* [<span data-ttu-id="f1854-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1854-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="f1854-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f1854-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/jdacloud-tutorial/tutorial_general_01.png
[2]: ./media/jdacloud-tutorial/tutorial_general_02.png
[3]: ./media/jdacloud-tutorial/tutorial_general_03.png
[4]: ./media/jdacloud-tutorial/tutorial_general_04.png

[100]: ./media/jdacloud-tutorial/tutorial_general_100.png

[200]: ./media/jdacloud-tutorial/tutorial_general_200.png
[201]: ./media/jdacloud-tutorial/tutorial_general_201.png
[202]: ./media/jdacloud-tutorial/tutorial_general_202.png
[203]: ./media/jdacloud-tutorial/tutorial_general_203.png