---
title: 'Tutorial: Azure Active Directory integration with Greenhouse | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Greenhouse.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 78ec1766-4f79-4f16-9a66-d5584c4b6151
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 7f48a0c11beb038370a8fc00e64d87127d356dec
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857402"
---
# <a name="tutorial-azure-active-directory-integration-with-greenhouse"></a><span data-ttu-id="5b111-103">Tutorial: Azure Active Directory integration with Greenhouse</span><span class="sxs-lookup"><span data-stu-id="5b111-103">Tutorial: Azure Active Directory integration with Greenhouse</span></span>

<span data-ttu-id="5b111-104">In this tutorial, you learn how to integrate Greenhouse with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5b111-104">In this tutorial, you learn how to integrate Greenhouse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b111-105">Integrating Greenhouse with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="5b111-105">Integrating Greenhouse with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5b111-106">You can control in Azure AD who has access to Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="5b111-106">You can control in Azure AD who has access to Greenhouse.</span></span>
- <span data-ttu-id="5b111-107">You can enable your users to automatically get signed-on to Greenhouse (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="5b111-107">You can enable your users to automatically get signed-on to Greenhouse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5b111-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5b111-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="5b111-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="5b111-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b111-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5b111-110">Prerequisites</span></span>

<span data-ttu-id="5b111-111">To configure Azure AD integration with Greenhouse, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="5b111-111">To configure Azure AD integration with Greenhouse, you need the following items:</span></span>

- <span data-ttu-id="5b111-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="5b111-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b111-113">A Greenhouse single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="5b111-113">A Greenhouse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5b111-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="5b111-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5b111-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="5b111-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b111-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="5b111-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5b111-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b111-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5b111-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="5b111-118">Scenario description</span></span>
<span data-ttu-id="5b111-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="5b111-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b111-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="5b111-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b111-121">Adding Greenhouse from the gallery</span><span class="sxs-lookup"><span data-stu-id="5b111-121">Adding Greenhouse from the gallery</span></span>
1. <span data-ttu-id="5b111-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5b111-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-greenhouse-from-the-gallery"></a><span data-ttu-id="5b111-123">Adding Greenhouse from the gallery</span><span class="sxs-lookup"><span data-stu-id="5b111-123">Adding Greenhouse from the gallery</span></span>
<span data-ttu-id="5b111-124">To configure the integration of Greenhouse into Azure AD, you need to add Greenhouse from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="5b111-124">To configure the integration of Greenhouse into Azure AD, you need to add Greenhouse from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5b111-125">**To add Greenhouse from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5b111-125">**To add Greenhouse from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5b111-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="5b111-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="5b111-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="5b111-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5b111-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="5b111-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="5b111-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="5b111-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="5b111-133">In the search box, type **Greenhouse**, select **Greenhouse** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="5b111-133">In the search box, type **Greenhouse**, select **Greenhouse** from result panel then click **Add** button to add the application.</span></span>

    ![Greenhouse in the results list](./media/greenhouse-tutorial/tutorial_greenhouse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5b111-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5b111-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5b111-136">In this section, you configure and test Azure AD single sign-on with Greenhouse based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5b111-136">In this section, you configure and test Azure AD single sign-on with Greenhouse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5b111-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Greenhouse is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b111-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Greenhouse is to a user in Azure AD.</span></span> <span data-ttu-id="5b111-138">In other words, a link relationship between an Azure AD user and the related user in Greenhouse needs to be established.</span><span class="sxs-lookup"><span data-stu-id="5b111-138">In other words, a link relationship between an Azure AD user and the related user in Greenhouse needs to be established.</span></span>

<span data-ttu-id="5b111-139">In Greenhouse, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="5b111-139">In Greenhouse, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5b111-140">To configure and test Azure AD single sign-on with Greenhouse, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="5b111-140">To configure and test Azure AD single sign-on with Greenhouse, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5b111-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="5b111-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="5b111-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b111-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="5b111-143">**[Create a Greenhouse test user](#create-a-greenhouse-test-user)** - to have a counterpart of Britta Simon in Greenhouse that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="5b111-143">**[Create a Greenhouse test user](#create-a-greenhouse-test-user)** - to have a counterpart of Britta Simon in Greenhouse that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="5b111-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5b111-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="5b111-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="5b111-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5b111-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5b111-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5b111-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Greenhouse application.</span><span class="sxs-lookup"><span data-stu-id="5b111-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Greenhouse application.</span></span>

<span data-ttu-id="5b111-148">**To configure Azure AD single sign-on with Greenhouse, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5b111-148">**To configure Azure AD single sign-on with Greenhouse, perform the following steps:**</span></span>

1. <span data-ttu-id="5b111-149">In the Azure portal, on the **Greenhouse** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5b111-149">In the Azure portal, on the **Greenhouse** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="5b111-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5b111-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/greenhouse-tutorial/tutorial_greenhouse_samlbase.png)

1. <span data-ttu-id="5b111-153">On the **Greenhouse Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5b111-153">On the **Greenhouse Domain and URLs** section, perform the following steps:</span></span>

    ![Greenhouse Domain and URLs single sign-on information](./media/greenhouse-tutorial/tutorial_greenhouse_url.png)

    <span data-ttu-id="5b111-155">a.</span><span class="sxs-lookup"><span data-stu-id="5b111-155">a.</span></span> <span data-ttu-id="5b111-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="5b111-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.greenhouse.io`</span></span>

    <span data-ttu-id="5b111-157">b.</span><span class="sxs-lookup"><span data-stu-id="5b111-157">b.</span></span> <span data-ttu-id="5b111-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="5b111-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.greenhouse.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5b111-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="5b111-159">These values are not real.</span></span> <span data-ttu-id="5b111-160">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="5b111-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5b111-161">Contact [Greenhouse Client support team](https://www.greenhouse.io/contact) to get these values.</span><span class="sxs-lookup"><span data-stu-id="5b111-161">Contact [Greenhouse Client support team](https://www.greenhouse.io/contact) to get these values.</span></span> 
 


1. <span data-ttu-id="5b111-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="5b111-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/greenhouse-tutorial/tutorial_greenhouse_certificate.png) 

1. <span data-ttu-id="5b111-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="5b111-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/greenhouse-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="5b111-166">To configure single sign-on on **Greenhouse** side, you need to send the downloaded **Metadata XML** to [Greenhouse support team](http://www.greenhouse.io/contact).</span><span class="sxs-lookup"><span data-stu-id="5b111-166">To configure single sign-on on **Greenhouse** side, you need to send the downloaded **Metadata XML** to [Greenhouse support team](http://www.greenhouse.io/contact).</span></span>

> [!TIP]
> <span data-ttu-id="5b111-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="5b111-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5b111-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="5b111-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5b111-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5b111-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5b111-170">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5b111-170">Create an Azure AD test user</span></span>

<span data-ttu-id="5b111-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b111-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="5b111-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5b111-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5b111-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="5b111-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/greenhouse-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="5b111-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="5b111-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/greenhouse-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="5b111-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="5b111-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/greenhouse-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="5b111-180">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5b111-180">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/greenhouse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5b111-182">a.</span><span class="sxs-lookup"><span data-stu-id="5b111-182">a.</span></span> <span data-ttu-id="5b111-183">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5b111-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b111-184">b.</span><span class="sxs-lookup"><span data-stu-id="5b111-184">b.</span></span> <span data-ttu-id="5b111-185">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b111-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="5b111-186">c.</span><span class="sxs-lookup"><span data-stu-id="5b111-186">c.</span></span> <span data-ttu-id="5b111-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="5b111-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="5b111-188">d.</span><span class="sxs-lookup"><span data-stu-id="5b111-188">d.</span></span> <span data-ttu-id="5b111-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5b111-189">Click **Create**.</span></span>
 
### <a name="create-a-greenhouse-test-user"></a><span data-ttu-id="5b111-190">Create a Greenhouse test user</span><span class="sxs-lookup"><span data-stu-id="5b111-190">Create a Greenhouse test user</span></span>

<span data-ttu-id="5b111-191">In order to enable Azure AD users to log into Greenhouse, they must be provisioned into Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="5b111-191">In order to enable Azure AD users to log into Greenhouse, they must be provisioned into Greenhouse.</span></span> <span data-ttu-id="5b111-192">In the case of Greenhouse, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="5b111-192">In the case of Greenhouse, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="5b111-193">You can use any other Greenhouse user account creation tools or APIs provided by Greenhouse to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="5b111-193">You can use any other Greenhouse user account creation tools or APIs provided by Greenhouse to provision AAD user accounts.</span></span> 

<span data-ttu-id="5b111-194">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5b111-194">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="5b111-195">Log in to your **Greenhouse** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="5b111-195">Log in to your **Greenhouse** company site as an administrator.</span></span>

1. <span data-ttu-id="5b111-196">In the menu on the top, click **Configure**, and then click **Users**.</span><span class="sxs-lookup"><span data-stu-id="5b111-196">In the menu on the top, click **Configure**, and then click **Users**.</span></span>
   
   <span data-ttu-id="5b111-197">![Users](./media/greenhouse-tutorial/ic790791.png "Users")</span><span class="sxs-lookup"><span data-stu-id="5b111-197">![Users](./media/greenhouse-tutorial/ic790791.png "Users")</span></span>

1. <span data-ttu-id="5b111-198">Click **New Users**.</span><span class="sxs-lookup"><span data-stu-id="5b111-198">Click **New Users**.</span></span>
   
   <span data-ttu-id="5b111-199">![New User](./media/greenhouse-tutorial/ic790792.png "New User")</span><span class="sxs-lookup"><span data-stu-id="5b111-199">![New User](./media/greenhouse-tutorial/ic790792.png "New User")</span></span>

1. <span data-ttu-id="5b111-200">In the **Add New User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5b111-200">In the **Add New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="5b111-201">![Add New User](./media/greenhouse-tutorial/ic790793.png "Add New User")</span><span class="sxs-lookup"><span data-stu-id="5b111-201">![Add New User](./media/greenhouse-tutorial/ic790793.png "Add New User")</span></span>

   <span data-ttu-id="5b111-202">a.</span><span class="sxs-lookup"><span data-stu-id="5b111-202">a.</span></span> <span data-ttu-id="5b111-203">In the **Enter user emails** textbox, type the email address of a valid Azure Active Directory account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="5b111-203">In the **Enter user emails** textbox, type the email address of a valid Azure Active Directory account you want to provision.</span></span>

   <span data-ttu-id="5b111-204">b.</span><span class="sxs-lookup"><span data-stu-id="5b111-204">b.</span></span> <span data-ttu-id="5b111-205">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="5b111-205">Click **Save**.</span></span>    
   
      >[!NOTE]
      ><span data-ttu-id="5b111-206">The Azure Active Directory account holders will receive an email including a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="5b111-206">The Azure Active Directory account holders will receive an email including a link to confirm the account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5b111-207">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5b111-207">Assign the Azure AD test user</span></span>

<span data-ttu-id="5b111-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="5b111-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Greenhouse.</span></span>

![Assign the user role][200] 

<span data-ttu-id="5b111-210">**To assign Britta Simon to Greenhouse, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5b111-210">**To assign Britta Simon to Greenhouse, perform the following steps:**</span></span>

1. <span data-ttu-id="5b111-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="5b111-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="5b111-213">In the applications list, select **Greenhouse**.</span><span class="sxs-lookup"><span data-stu-id="5b111-213">In the applications list, select **Greenhouse**.</span></span>

    ![The Greenhouse link in the Applications list](./media/greenhouse-tutorial/tutorial_greenhouse_app.png)  

1. <span data-ttu-id="5b111-215">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="5b111-215">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="5b111-217">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="5b111-217">Click **Add** button.</span></span> <span data-ttu-id="5b111-218">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="5b111-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="5b111-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="5b111-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="5b111-221">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="5b111-221">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="5b111-222">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="5b111-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5b111-223">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="5b111-223">Test single sign-on</span></span>

<span data-ttu-id="5b111-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="5b111-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5b111-225">When you click the Greenhouse tile in the Access Panel, you should get automatically signed-on to your Greenhouse application.</span><span class="sxs-lookup"><span data-stu-id="5b111-225">When you click the Greenhouse tile in the Access Panel, you should get automatically signed-on to your Greenhouse application.</span></span>
<span data-ttu-id="5b111-226">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5b111-226">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5b111-227">Additional resources</span><span class="sxs-lookup"><span data-stu-id="5b111-227">Additional resources</span></span>

* [<span data-ttu-id="5b111-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b111-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="5b111-229">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5b111-229">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/greenhouse-tutorial/tutorial_general_01.png
[2]: ./media/greenhouse-tutorial/tutorial_general_02.png
[3]: ./media/greenhouse-tutorial/tutorial_general_03.png
[4]: ./media/greenhouse-tutorial/tutorial_general_04.png

[100]: ./media/greenhouse-tutorial/tutorial_general_100.png

[200]: ./media/greenhouse-tutorial/tutorial_general_200.png
[201]: ./media/greenhouse-tutorial/tutorial_general_201.png
[202]: ./media/greenhouse-tutorial/tutorial_general_202.png
[203]: ./media/greenhouse-tutorial/tutorial_general_203.png

