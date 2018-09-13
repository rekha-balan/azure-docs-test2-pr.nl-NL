---
title: 'Tutorial: Azure Active Directory integration with MobileIron | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and MobileIron.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 3e4bbd5b-290e-4951-971b-ec0c1c11aaa2
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/9/2017
ms.author: jeedes
ms.openlocfilehash: 53cec59841fbda49e4e410f069882ea76996f9fb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857742"
---
# <a name="tutorial-azure-active-directory-integration-with-mobileiron"></a><span data-ttu-id="f8f2e-103">Tutorial: Azure Active Directory integration with MobileIron</span><span class="sxs-lookup"><span data-stu-id="f8f2e-103">Tutorial: Azure Active Directory integration with MobileIron</span></span>

<span data-ttu-id="f8f2e-104">In this tutorial, you learn how to integrate MobileIron with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f8f2e-104">In this tutorial, you learn how to integrate MobileIron with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f8f2e-105">Integrating MobileIron with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f8f2e-105">Integrating MobileIron with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f8f2e-106">You can control in Azure AD who has access to MobileIron.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-106">You can control in Azure AD who has access to MobileIron.</span></span>
- <span data-ttu-id="f8f2e-107">You can enable your users to automatically get signed-on to MobileIron (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-107">You can enable your users to automatically get signed-on to MobileIron (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f8f2e-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f8f2e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="f8f2e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8f2e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f8f2e-110">Prerequisites</span></span>

<span data-ttu-id="f8f2e-111">To configure Azure AD integration with MobileIron, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f8f2e-111">To configure Azure AD integration with MobileIron, you need the following items:</span></span>

- <span data-ttu-id="f8f2e-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f8f2e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f8f2e-113">A MobileIron single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f8f2e-113">A MobileIron single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f8f2e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f8f2e-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f8f2e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f8f2e-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f8f2e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f8f2e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f8f2e-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f8f2e-118">Scenario description</span></span>
<span data-ttu-id="f8f2e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f8f2e-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f8f2e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f8f2e-121">Adding MobileIron from the gallery</span><span class="sxs-lookup"><span data-stu-id="f8f2e-121">Adding MobileIron from the gallery</span></span>
1. <span data-ttu-id="f8f2e-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f8f2e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mobileiron-from-the-gallery"></a><span data-ttu-id="f8f2e-123">Adding MobileIron from the gallery</span><span class="sxs-lookup"><span data-stu-id="f8f2e-123">Adding MobileIron from the gallery</span></span>
<span data-ttu-id="f8f2e-124">To configure the integration of MobileIron into Azure AD, you need to add MobileIron from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-124">To configure the integration of MobileIron into Azure AD, you need to add MobileIron from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f8f2e-125">**To add MobileIron from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f8f2e-125">**To add MobileIron from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f8f2e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="f8f2e-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f8f2e-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="f8f2e-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="f8f2e-133">In the search box, type **MobileIron**, select **MobileIron** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-133">In the search box, type **MobileIron**, select **MobileIron** from result panel then click **Add** button to add the application.</span></span>

    ![MobileIron in the results list](./media/mobileiron-tutorial/tutorial_mobileiron_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f8f2e-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f8f2e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f8f2e-136">In this section, you configure and test Azure AD single sign-on with MobileIron based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="f8f2e-136">In this section, you configure and test Azure AD single sign-on with MobileIron based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f8f2e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in MobileIron is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in MobileIron is to a user in Azure AD.</span></span> <span data-ttu-id="f8f2e-138">In other words, a link relationship between an Azure AD user and the related user in MobileIron needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-138">In other words, a link relationship between an Azure AD user and the related user in MobileIron needs to be established.</span></span>

<span data-ttu-id="f8f2e-139">In MobileIron, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-139">In MobileIron, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f8f2e-140">To configure and test Azure AD single sign-on with MobileIron, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f8f2e-140">To configure and test Azure AD single sign-on with MobileIron, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f8f2e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="f8f2e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="f8f2e-143">**[Create a MobileIron test user](#create-a-mobileiron-test-user)** - to have a counterpart of Britta Simon in MobileIron that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-143">**[Create a MobileIron test user](#create-a-mobileiron-test-user)** - to have a counterpart of Britta Simon in MobileIron that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="f8f2e-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="f8f2e-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f8f2e-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f8f2e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f8f2e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MobileIron application.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MobileIron application.</span></span>

<span data-ttu-id="f8f2e-148">**To configure Azure AD single sign-on with MobileIron, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f8f2e-148">**To configure Azure AD single sign-on with MobileIron, perform the following steps:**</span></span>

1. <span data-ttu-id="f8f2e-149">In the Azure portal, on the **MobileIron** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-149">In the Azure portal, on the **MobileIron** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="f8f2e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/mobileiron-tutorial/tutorial_mobileiron_samlbase.png)

1. <span data-ttu-id="f8f2e-153">On the **MobileIron Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="f8f2e-153">On the **MobileIron Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![MobileIron Domain and URLs single sign-on information](./media/mobileiron-tutorial/tutorial_mobileiron_url.png)

    <span data-ttu-id="f8f2e-155">a.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-155">a.</span></span> <span data-ttu-id="f8f2e-156">In the **Identifier** textbox, type a URL using the following pattern: `https://www.mobileiron.com/<key>`</span><span class="sxs-lookup"><span data-stu-id="f8f2e-156">In the **Identifier** textbox, type a URL using the following pattern: `https://www.mobileiron.com/<key>`</span></span>

    <span data-ttu-id="f8f2e-157">b.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-157">b.</span></span> <span data-ttu-id="f8f2e-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<host>.mobileiron.com/saml/SSO/alias/<key>`</span><span class="sxs-lookup"><span data-stu-id="f8f2e-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<host>.mobileiron.com/saml/SSO/alias/<key>`</span></span>

1. <span data-ttu-id="f8f2e-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="f8f2e-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![MobileIron Domain and URLs single sign-on](./media/mobileiron-tutorial/tutorial_mobileiron_url1.png)

    <span data-ttu-id="f8f2e-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<host>.mobileiron.com/user/login.html`</span><span class="sxs-lookup"><span data-stu-id="f8f2e-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<host>.mobileiron.com/user/login.html`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="f8f2e-162">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-162">These values are not real.</span></span> <span data-ttu-id="f8f2e-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="f8f2e-164">You will get the values of key and host from the administrative portal of MobileIron which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-164">You will get the values of key and host from the administrative portal of MobileIron which is explained later in the tutorial.</span></span>

1. <span data-ttu-id="f8f2e-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/mobileiron-tutorial/tutorial_mobileiron_certificate.png) 

1. <span data-ttu-id="f8f2e-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/mobileiron-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="f8f2e-169">In a different web browser window, log in to your MobileIron company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-169">In a different web browser window, log in to your MobileIron company site as an administrator.</span></span>

1. <span data-ttu-id="f8f2e-170">Go to **Admin** > **Identity**.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-170">Go to **Admin** > **Identity**.</span></span>

   * <span data-ttu-id="f8f2e-171">Select **AAD** option in the **Info on Cloud IDP Setup** field.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-171">Select **AAD** option in the **Info on Cloud IDP Setup** field.</span></span>

    ![Configure Single Sign-On Admin button](./media/mobileiron-tutorial/tutorial_mobileiron_admin.png)

1. <span data-ttu-id="f8f2e-173">Copy the values of **Key** and **Host** and paste them to complete the URLs in the **MobileIron Domain and URLs** section in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-173">Copy the values of **Key** and **Host** and paste them to complete the URLs in the **MobileIron Domain and URLs** section in Azure portal.</span></span>

    ![Configure Single Sign-On Admin button](./media/mobileiron-tutorial/key.png)

1. <span data-ttu-id="f8f2e-175">In the **Export metadata file from AAD and import to MobileIron Cloud Field** click **Choose File** to upload the downloaded metadata from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-175">In the **Export metadata file from AAD and import to MobileIron Cloud Field** click **Choose File** to upload the downloaded metadata from Azure portal.</span></span> <span data-ttu-id="f8f2e-176">Click **Done** once uploaded.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-176">Click **Done** once uploaded.</span></span>
 
    ![Configure Single Sign-On admin metadata button](./media/mobileiron-tutorial/tutorial_mobileiron_adminmetadata.png)

> [!TIP]
> <span data-ttu-id="f8f2e-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="f8f2e-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f8f2e-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f8f2e-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f8f2e-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f8f2e-181">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f8f2e-181">Create an Azure AD test user</span></span>

<span data-ttu-id="f8f2e-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="f8f2e-184">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f8f2e-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f8f2e-185">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-185">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/mobileiron-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="f8f2e-187">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-187">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/mobileiron-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="f8f2e-189">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-189">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/mobileiron-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="f8f2e-191">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f8f2e-191">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/mobileiron-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f8f2e-193">a.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-193">a.</span></span> <span data-ttu-id="f8f2e-194">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-194">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f8f2e-195">b.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-195">b.</span></span> <span data-ttu-id="f8f2e-196">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-196">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f8f2e-197">c.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-197">c.</span></span> <span data-ttu-id="f8f2e-198">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-198">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f8f2e-199">d.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-199">d.</span></span> <span data-ttu-id="f8f2e-200">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-200">Click **Create**.</span></span>
  
### <a name="create-a-mobileiron-test-user"></a><span data-ttu-id="f8f2e-201">Create a MobileIron test user</span><span class="sxs-lookup"><span data-stu-id="f8f2e-201">Create a MobileIron test user</span></span>

<span data-ttu-id="f8f2e-202">To enable Azure AD users to log in to MobileIron, they must be provisioned into MobileIron.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-202">To enable Azure AD users to log in to MobileIron, they must be provisioned into MobileIron.</span></span>  
<span data-ttu-id="f8f2e-203">In the case of MobileIron, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-203">In the case of MobileIron, provisioning is a manual task.</span></span>

<span data-ttu-id="f8f2e-204">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f8f2e-204">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="f8f2e-205">Log in to your MobileIron company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-205">Log in to your MobileIron company site as an administrator.</span></span>

1. <span data-ttu-id="f8f2e-206">Go to **Users** and Click on **Add** > **Single User**.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-206">Go to **Users** and Click on **Add** > **Single User**.</span></span>

    ![Configure Single Sign-On user button](./media/mobileiron-tutorial/tutorial_mobileiron_user.png)

1. <span data-ttu-id="f8f2e-208">On the **“Single User”** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f8f2e-208">On the **“Single User”** dialog page, perform the following steps:</span></span>

    ![Configure Single Sign-On user add button](./media/mobileiron-tutorial/tutorial_mobileiron_useradd.png)

    <span data-ttu-id="f8f2e-210">a.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-210">a.</span></span> <span data-ttu-id="f8f2e-211">In **E-mail Address** text box, enter the email of user like brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-211">In **E-mail Address** text box, enter the email of user like brittasimon@contoso.com.</span></span>

    <span data-ttu-id="f8f2e-212">b.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-212">b.</span></span> <span data-ttu-id="f8f2e-213">In **First Name** text box, enter the first name of user like Britta.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-213">In **First Name** text box, enter the first name of user like Britta.</span></span>

    <span data-ttu-id="f8f2e-214">c.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-214">c.</span></span> <span data-ttu-id="f8f2e-215">In **Last Name** text box, enter the last name of user like Simon.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-215">In **Last Name** text box, enter the last name of user like Simon.</span></span>
    
    <span data-ttu-id="f8f2e-216">d.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-216">d.</span></span> <span data-ttu-id="f8f2e-217">Click **Done**.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-217">Click **Done**.</span></span>  

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f8f2e-218">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f8f2e-218">Assign the Azure AD test user</span></span>

<span data-ttu-id="f8f2e-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MobileIron.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MobileIron.</span></span>

![Assign the user role][200] 

<span data-ttu-id="f8f2e-221">**To assign Britta Simon to MobileIron, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f8f2e-221">**To assign Britta Simon to MobileIron, perform the following steps:**</span></span>

1. <span data-ttu-id="f8f2e-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="f8f2e-224">In the applications list, select **MobileIron**.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-224">In the applications list, select **MobileIron**.</span></span>

    ![The MobileIron link in the Applications list](./media/mobileiron-tutorial/tutorial_mobileiron_app.png)  

1. <span data-ttu-id="f8f2e-226">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-226">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="f8f2e-228">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-228">Click **Add** button.</span></span> <span data-ttu-id="f8f2e-229">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="f8f2e-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="f8f2e-232">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-232">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="f8f2e-233">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f8f2e-234">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="f8f2e-234">Test single sign-on</span></span>

<span data-ttu-id="f8f2e-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f8f2e-236">When you click the MobileIron tile in the Access Panel, you should get automatically signed-on to your MobileIron application.</span><span class="sxs-lookup"><span data-stu-id="f8f2e-236">When you click the MobileIron tile in the Access Panel, you should get automatically signed-on to your MobileIron application.</span></span>
<span data-ttu-id="f8f2e-237">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f8f2e-237">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f8f2e-238">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f8f2e-238">Additional resources</span></span>

* [<span data-ttu-id="f8f2e-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f8f2e-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="f8f2e-240">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f8f2e-240">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)


<!--Image references-->

[1]: ./media/mobileiron-tutorial/tutorial_general_01.png
[2]: ./media/mobileiron-tutorial/tutorial_general_02.png
[3]: ./media/mobileiron-tutorial/tutorial_general_03.png
[4]: ./media/mobileiron-tutorial/tutorial_general_04.png

[100]: ./media/mobileiron-tutorial/tutorial_general_100.png

[200]: ./media/mobileiron-tutorial/tutorial_general_200.png
[201]: ./media/mobileiron-tutorial/tutorial_general_201.png
[202]: ./media/mobileiron-tutorial/tutorial_general_202.png
[203]: ./media/mobileiron-tutorial/tutorial_general_203.png

