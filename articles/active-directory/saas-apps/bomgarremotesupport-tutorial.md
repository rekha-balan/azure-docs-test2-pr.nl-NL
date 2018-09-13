---
title: 'Tutorial: Azure Active Directory integration with Bomgar Remote Support | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Bomgar Remote Support.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 193b163f-bdee-4974-b16d-777c51b991df
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2018
ms.author: jeedes
ms.openlocfilehash: c59f4291726b24b7c96bb60d0497c1578a3e4b0f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965545"
---
# <a name="tutorial-azure-active-directory-integration-with-bomgar-remote-support"></a><span data-ttu-id="47cc0-103">Tutorial: Azure Active Directory integration with Bomgar Remote Support</span><span class="sxs-lookup"><span data-stu-id="47cc0-103">Tutorial: Azure Active Directory integration with Bomgar Remote Support</span></span>

<span data-ttu-id="47cc0-104">In this tutorial, you learn how to integrate Bomgar Remote Support with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="47cc0-104">In this tutorial, you learn how to integrate Bomgar Remote Support with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="47cc0-105">Integrating Bomgar Remote Support with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="47cc0-105">Integrating Bomgar Remote Support with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="47cc0-106">You can control in Azure AD who has access to Bomgar Remote Support.</span><span class="sxs-lookup"><span data-stu-id="47cc0-106">You can control in Azure AD who has access to Bomgar Remote Support.</span></span>
- <span data-ttu-id="47cc0-107">You can enable your users to automatically get signed-on to Bomgar Remote Support (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="47cc0-107">You can enable your users to automatically get signed-on to Bomgar Remote Support (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="47cc0-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="47cc0-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="47cc0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="47cc0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47cc0-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="47cc0-110">Prerequisites</span></span>

<span data-ttu-id="47cc0-111">To configure Azure AD integration with Bomgar Remote Support, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="47cc0-111">To configure Azure AD integration with Bomgar Remote Support, you need the following items:</span></span>

- <span data-ttu-id="47cc0-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="47cc0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="47cc0-113">A Bomgar Remote Support single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="47cc0-113">A Bomgar Remote Support single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="47cc0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="47cc0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="47cc0-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="47cc0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="47cc0-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="47cc0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="47cc0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="47cc0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="47cc0-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="47cc0-118">Scenario description</span></span>
<span data-ttu-id="47cc0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="47cc0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="47cc0-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="47cc0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="47cc0-121">Adding Bomgar Remote Support from the gallery</span><span class="sxs-lookup"><span data-stu-id="47cc0-121">Adding Bomgar Remote Support from the gallery</span></span>
2. <span data-ttu-id="47cc0-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="47cc0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bomgar-remote-support-from-the-gallery"></a><span data-ttu-id="47cc0-123">Adding Bomgar Remote Support from the gallery</span><span class="sxs-lookup"><span data-stu-id="47cc0-123">Adding Bomgar Remote Support from the gallery</span></span>
<span data-ttu-id="47cc0-124">To configure the integration of Bomgar Remote Support into Azure AD, you need to add Bomgar Remote Support from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="47cc0-124">To configure the integration of Bomgar Remote Support into Azure AD, you need to add Bomgar Remote Support from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="47cc0-125">**To add Bomgar Remote Support from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="47cc0-125">**To add Bomgar Remote Support from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="47cc0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="47cc0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="47cc0-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="47cc0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="47cc0-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="47cc0-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="47cc0-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="47cc0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="47cc0-133">In the search box, type **Bomgar Remote Support**, select **Bomgar Remote Support** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="47cc0-133">In the search box, type **Bomgar Remote Support**, select **Bomgar Remote Support** from result panel then click **Add** button to add the application.</span></span>

    ![Bomgar Remote Support in the results list](./media/bomgarremotesupport-tutorial/tutorial_bomgarremotesupport_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="47cc0-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="47cc0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="47cc0-136">In this section, you configure and test Azure AD single sign-on with Bomgar Remote Support based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="47cc0-136">In this section, you configure and test Azure AD single sign-on with Bomgar Remote Support based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="47cc0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Bomgar Remote Support is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47cc0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Bomgar Remote Support is to a user in Azure AD.</span></span> <span data-ttu-id="47cc0-138">In other words, a link relationship between an Azure AD user and the related user in Bomgar Remote Support needs to be established.</span><span class="sxs-lookup"><span data-stu-id="47cc0-138">In other words, a link relationship between an Azure AD user and the related user in Bomgar Remote Support needs to be established.</span></span>

<span data-ttu-id="47cc0-139">To configure and test Azure AD single sign-on with Bomgar Remote Support, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="47cc0-139">To configure and test Azure AD single sign-on with Bomgar Remote Support, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="47cc0-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="47cc0-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="47cc0-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="47cc0-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="47cc0-142">**[Create a Bomgar Remote Support test user](#create-a-bomgar-remote-support-test-user)** - to have a counterpart of Britta Simon in Bomgar Remote Support that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="47cc0-142">**[Create a Bomgar Remote Support test user](#create-a-bomgar-remote-support-test-user)** - to have a counterpart of Britta Simon in Bomgar Remote Support that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="47cc0-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="47cc0-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="47cc0-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="47cc0-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="47cc0-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="47cc0-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="47cc0-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bomgar Remote Support application.</span><span class="sxs-lookup"><span data-stu-id="47cc0-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bomgar Remote Support application.</span></span>

<span data-ttu-id="47cc0-147">**To configure Azure AD single sign-on with Bomgar Remote Support, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="47cc0-147">**To configure Azure AD single sign-on with Bomgar Remote Support, perform the following steps:**</span></span>

1. <span data-ttu-id="47cc0-148">In the Azure portal, on the **Bomgar Remote Support** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="47cc0-148">In the Azure portal, on the **Bomgar Remote Support** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="47cc0-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="47cc0-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/bomgarremotesupport-tutorial/tutorial_bomgarremotesupport_samlbase.png)

3. <span data-ttu-id="47cc0-152">On the **Bomgar Remote Support Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="47cc0-152">On the **Bomgar Remote Support Domain and URLs** section, perform the following steps:</span></span>

    ![Bomgar Remote Support Domain and URLs single sign-on information](./media/bomgarremotesupport-tutorial/tutorial_bomgarremotesupport_url.png)

    <span data-ttu-id="47cc0-154">a.</span><span class="sxs-lookup"><span data-stu-id="47cc0-154">a.</span></span> <span data-ttu-id="47cc0-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.trafficmanager.net/saml`</span><span class="sxs-lookup"><span data-stu-id="47cc0-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.trafficmanager.net/saml`</span></span>

    <span data-ttu-id="47cc0-156">b.</span><span class="sxs-lookup"><span data-stu-id="47cc0-156">b.</span></span> <span data-ttu-id="47cc0-157">In the **Identifier (Entity ID)** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.trafficmanager.net`</span><span class="sxs-lookup"><span data-stu-id="47cc0-157">In the **Identifier (Entity ID)** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.trafficmanager.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="47cc0-158">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="47cc0-158">These values are not real.</span></span> <span data-ttu-id="47cc0-159">Update these values with the actual Sign-On URL and Identifier (Entity ID).</span><span class="sxs-lookup"><span data-stu-id="47cc0-159">Update these values with the actual Sign-On URL and Identifier (Entity ID).</span></span> <span data-ttu-id="47cc0-160">Contact [Bomgar Remote Support Client support team](https://www.bomgar.com/docs/index.htm#support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="47cc0-160">Contact [Bomgar Remote Support Client support team](https://www.bomgar.com/docs/index.htm#support) to get these values.</span></span> 
 
4. <span data-ttu-id="47cc0-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="47cc0-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/bomgarremotesupport-tutorial/tutorial_bomgarremotesupport_certificate.png) 

5. <span data-ttu-id="47cc0-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="47cc0-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/bomgarremotesupport-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="47cc0-165">To configure single sign-on on **Bomgar Remote Support** side, you need to send the downloaded **Metadata XML** to [Bomgar Remote Support support team](https://www.bomgar.com/docs/index.htm#support).</span><span class="sxs-lookup"><span data-stu-id="47cc0-165">To configure single sign-on on **Bomgar Remote Support** side, you need to send the downloaded **Metadata XML** to [Bomgar Remote Support support team](https://www.bomgar.com/docs/index.htm#support).</span></span> <span data-ttu-id="47cc0-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="47cc0-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="47cc0-167">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="47cc0-167">Create an Azure AD test user</span></span>

<span data-ttu-id="47cc0-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="47cc0-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="47cc0-170">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="47cc0-170">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="47cc0-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="47cc0-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/bomgarremotesupport-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="47cc0-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="47cc0-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/bomgarremotesupport-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="47cc0-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="47cc0-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/bomgarremotesupport-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="47cc0-177">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="47cc0-177">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/bomgarremotesupport-tutorial/create_aaduser_04.png)

    <span data-ttu-id="47cc0-179">a.</span><span class="sxs-lookup"><span data-stu-id="47cc0-179">a.</span></span> <span data-ttu-id="47cc0-180">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="47cc0-180">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="47cc0-181">b.</span><span class="sxs-lookup"><span data-stu-id="47cc0-181">b.</span></span> <span data-ttu-id="47cc0-182">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="47cc0-182">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="47cc0-183">c.</span><span class="sxs-lookup"><span data-stu-id="47cc0-183">c.</span></span> <span data-ttu-id="47cc0-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="47cc0-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="47cc0-185">d.</span><span class="sxs-lookup"><span data-stu-id="47cc0-185">d.</span></span> <span data-ttu-id="47cc0-186">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="47cc0-186">Click **Create**.</span></span>
 
### <a name="create-a-bomgar-remote-support-test-user"></a><span data-ttu-id="47cc0-187">Create a Bomgar Remote Support test user</span><span class="sxs-lookup"><span data-stu-id="47cc0-187">Create a Bomgar Remote Support test user</span></span>

<span data-ttu-id="47cc0-188">The objective of this section is to create a user called Britta Simon in Bomgar Remote Support.</span><span class="sxs-lookup"><span data-stu-id="47cc0-188">The objective of this section is to create a user called Britta Simon in Bomgar Remote Support.</span></span> <span data-ttu-id="47cc0-189">Bomgar Remote Support supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="47cc0-189">Bomgar Remote Support supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="47cc0-190">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="47cc0-190">There is no action item for you in this section.</span></span> <span data-ttu-id="47cc0-191">A new user is created during an attempt to access Bomgar Remote Support if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="47cc0-191">A new user is created during an attempt to access Bomgar Remote Support if it doesn't exist yet.</span></span>
>[!Note]
><span data-ttu-id="47cc0-192">If you need to create a user manually, contact [Bomgar Remote Support support team](https://www.bomgar.com/docs/index.htm#support).</span><span class="sxs-lookup"><span data-stu-id="47cc0-192">If you need to create a user manually, contact [Bomgar Remote Support support team](https://www.bomgar.com/docs/index.htm#support).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="47cc0-193">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="47cc0-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="47cc0-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bomgar Remote Support.</span><span class="sxs-lookup"><span data-stu-id="47cc0-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bomgar Remote Support.</span></span>

![Assign the user role][200] 

<span data-ttu-id="47cc0-196">**To assign Britta Simon to Bomgar Remote Support, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="47cc0-196">**To assign Britta Simon to Bomgar Remote Support, perform the following steps:**</span></span>

1. <span data-ttu-id="47cc0-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="47cc0-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="47cc0-199">In the applications list, select **Bomgar Remote Support**.</span><span class="sxs-lookup"><span data-stu-id="47cc0-199">In the applications list, select **Bomgar Remote Support**.</span></span>

    ![The Bomgar Remote Support link in the Applications list](./media/bomgarremotesupport-tutorial/tutorial_bomgarremotesupport_app.png)  

3. <span data-ttu-id="47cc0-201">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="47cc0-201">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="47cc0-203">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="47cc0-203">Click **Add** button.</span></span> <span data-ttu-id="47cc0-204">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="47cc0-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="47cc0-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="47cc0-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="47cc0-207">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="47cc0-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="47cc0-208">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="47cc0-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="47cc0-209">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="47cc0-209">Test single sign-on</span></span>

<span data-ttu-id="47cc0-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="47cc0-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="47cc0-211">When you click the Bomgar Remote Support tile in the Access Panel, you should get automatically signed-on to your Bomgar Remote Support application.</span><span class="sxs-lookup"><span data-stu-id="47cc0-211">When you click the Bomgar Remote Support tile in the Access Panel, you should get automatically signed-on to your Bomgar Remote Support application.</span></span>
<span data-ttu-id="47cc0-212">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="47cc0-212">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="47cc0-213">Additional resources</span><span class="sxs-lookup"><span data-stu-id="47cc0-213">Additional resources</span></span>

* [<span data-ttu-id="47cc0-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47cc0-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="47cc0-215">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="47cc0-215">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/bomgarremotesupport-tutorial/tutorial_general_01.png
[2]: ./media/bomgarremotesupport-tutorial/tutorial_general_02.png
[3]: ./media/bomgarremotesupport-tutorial/tutorial_general_03.png
[4]: ./media/bomgarremotesupport-tutorial/tutorial_general_04.png

[100]: ./media/bomgarremotesupport-tutorial/tutorial_general_100.png

[200]: ./media/bomgarremotesupport-tutorial/tutorial_general_200.png
[201]: ./media/bomgarremotesupport-tutorial/tutorial_general_201.png
[202]: ./media/bomgarremotesupport-tutorial/tutorial_general_202.png
[203]: ./media/bomgarremotesupport-tutorial/tutorial_general_203.png

