---
title: 'Tutorial: Azure Active Directory integration with Qualtrics | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Qualtrics.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2017
ms.author: jeedes
ms.openlocfilehash: 27f972ce789ae5bccf173138fe93de33de0d3932
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856504"
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="ead01-103">Tutorial: Azure Active Directory integration with Qualtrics</span><span class="sxs-lookup"><span data-stu-id="ead01-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>

<span data-ttu-id="ead01-104">In this tutorial, you learn how to integrate Qualtrics with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ead01-104">In this tutorial, you learn how to integrate Qualtrics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ead01-105">Integrating Qualtrics with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ead01-105">Integrating Qualtrics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ead01-106">You can control in Azure AD who has access to Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="ead01-106">You can control in Azure AD who has access to Qualtrics.</span></span>
- <span data-ttu-id="ead01-107">You can enable your users to automatically get signed-on to Qualtrics (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="ead01-107">You can enable your users to automatically get signed-on to Qualtrics (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ead01-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ead01-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="ead01-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="ead01-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ead01-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ead01-110">Prerequisites</span></span>

<span data-ttu-id="ead01-111">To configure Azure AD integration with Qualtrics, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ead01-111">To configure Azure AD integration with Qualtrics, you need the following items:</span></span>

- <span data-ttu-id="ead01-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ead01-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ead01-113">A Qualtrics single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ead01-113">A Qualtrics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ead01-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ead01-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ead01-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ead01-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ead01-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="ead01-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ead01-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ead01-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ead01-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="ead01-118">Scenario description</span></span>
<span data-ttu-id="ead01-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ead01-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ead01-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ead01-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ead01-121">Adding Qualtrics from the gallery</span><span class="sxs-lookup"><span data-stu-id="ead01-121">Adding Qualtrics from the gallery</span></span>
1. <span data-ttu-id="ead01-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ead01-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qualtrics-from-the-gallery"></a><span data-ttu-id="ead01-123">Adding Qualtrics from the gallery</span><span class="sxs-lookup"><span data-stu-id="ead01-123">Adding Qualtrics from the gallery</span></span>
<span data-ttu-id="ead01-124">To configure the integration of Qualtrics into Azure AD, you need to add Qualtrics from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ead01-124">To configure the integration of Qualtrics into Azure AD, you need to add Qualtrics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ead01-125">**To add Qualtrics from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ead01-125">**To add Qualtrics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ead01-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ead01-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="ead01-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="ead01-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ead01-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ead01-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="ead01-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="ead01-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="ead01-133">In the search box, type **Qualtrics**, select **Qualtrics** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="ead01-133">In the search box, type **Qualtrics**, select **Qualtrics** from result panel then click **Add** button to add the application.</span></span>

    ![Qualtrics in the results list](./media/qualtrics-tutorial/tutorial_qualtrics_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ead01-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ead01-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ead01-136">In this section, you configure and test Azure AD single sign-on with Qualtrics based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ead01-136">In this section, you configure and test Azure AD single sign-on with Qualtrics based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ead01-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Qualtrics is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ead01-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Qualtrics is to a user in Azure AD.</span></span> <span data-ttu-id="ead01-138">In other words, a link relationship between an Azure AD user and the related user in Qualtrics needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ead01-138">In other words, a link relationship between an Azure AD user and the related user in Qualtrics needs to be established.</span></span>

<span data-ttu-id="ead01-139">In Qualtrics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="ead01-139">In Qualtrics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ead01-140">To configure and test Azure AD single sign-on with Qualtrics, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ead01-140">To configure and test Azure AD single sign-on with Qualtrics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ead01-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ead01-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="ead01-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ead01-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="ead01-143">**[Create a Qualtrics test user](#create-a-qualtrics-test-user)** - to have a counterpart of Britta Simon in Qualtrics that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="ead01-143">**[Create a Qualtrics test user](#create-a-qualtrics-test-user)** - to have a counterpart of Britta Simon in Qualtrics that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="ead01-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ead01-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="ead01-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ead01-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ead01-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ead01-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ead01-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Qualtrics application.</span><span class="sxs-lookup"><span data-stu-id="ead01-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Qualtrics application.</span></span>

<span data-ttu-id="ead01-148">**To configure Azure AD single sign-on with Qualtrics, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ead01-148">**To configure Azure AD single sign-on with Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="ead01-149">In the Azure portal, on the **Qualtrics** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ead01-149">In the Azure portal, on the **Qualtrics** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="ead01-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ead01-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/qualtrics-tutorial/tutorial_qualtrics_samlbase.png)

1. <span data-ttu-id="ead01-153">On the **Qualtrics Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ead01-153">On the **Qualtrics Domain and URLs** section, perform the following steps:</span></span>

    ![Qualtrics Domain and URLs single sign-on information](./media/qualtrics-tutorial/tutorial_qualtrics_url.png)

    <span data-ttu-id="ead01-155">a.</span><span class="sxs-lookup"><span data-stu-id="ead01-155">a.</span></span> <span data-ttu-id="ead01-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.qualtrics.com`</span><span class="sxs-lookup"><span data-stu-id="ead01-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.qualtrics.com`</span></span>

    <span data-ttu-id="ead01-157">b.</span><span class="sxs-lookup"><span data-stu-id="ead01-157">b.</span></span> <span data-ttu-id="ead01-158">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="ead01-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.qualtrics.com/WRSAML/simplesaml/www/module.php/saml/sp/metadata.php/default-sp`|
    | `https://<companyname>.co1.qualtrics.com/WRSAML/simplesaml/www/module.php/saml/sp/metadata.php/default-sp`|

    > [!NOTE] 
    > <span data-ttu-id="ead01-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="ead01-159">These values are not real.</span></span> <span data-ttu-id="ead01-160">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="ead01-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ead01-161">Contact [Qualtrics Client support team](https://www.qualtrics.com/support/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="ead01-161">Contact [Qualtrics Client support team](https://www.qualtrics.com/support/) to get these values.</span></span>

1. <span data-ttu-id="ead01-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ead01-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/qualtrics-tutorial/tutorial_qualtrics_certificate.png) 

1. <span data-ttu-id="ead01-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="ead01-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/qualtrics-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="ead01-166">To configure single sign-on on **Qualtrics** side, you need to send the downloaded **Metadata XML** to [Qualtrics support team](https://www.qualtrics.com/support/).</span><span class="sxs-lookup"><span data-stu-id="ead01-166">To configure single sign-on on **Qualtrics** side, you need to send the downloaded **Metadata XML** to [Qualtrics support team](https://www.qualtrics.com/support/).</span></span> <span data-ttu-id="ead01-167">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="ead01-167">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ead01-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="ead01-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ead01-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="ead01-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ead01-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ead01-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ead01-171">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ead01-171">Create an Azure AD test user</span></span>

<span data-ttu-id="ead01-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ead01-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="ead01-174">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ead01-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ead01-175">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="ead01-175">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/qualtrics-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="ead01-177">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="ead01-177">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/qualtrics-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="ead01-179">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="ead01-179">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/qualtrics-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="ead01-181">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ead01-181">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/qualtrics-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ead01-183">a.</span><span class="sxs-lookup"><span data-stu-id="ead01-183">a.</span></span> <span data-ttu-id="ead01-184">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ead01-184">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ead01-185">b.</span><span class="sxs-lookup"><span data-stu-id="ead01-185">b.</span></span> <span data-ttu-id="ead01-186">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ead01-186">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="ead01-187">c.</span><span class="sxs-lookup"><span data-stu-id="ead01-187">c.</span></span> <span data-ttu-id="ead01-188">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="ead01-188">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="ead01-189">d.</span><span class="sxs-lookup"><span data-stu-id="ead01-189">d.</span></span> <span data-ttu-id="ead01-190">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ead01-190">Click **Create**.</span></span>
 
### <a name="create-a-qualtrics-test-user"></a><span data-ttu-id="ead01-191">Create a Qualtrics test user</span><span class="sxs-lookup"><span data-stu-id="ead01-191">Create a Qualtrics test user</span></span>

<span data-ttu-id="ead01-192">There is no action item for you to configure user provisioning to Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="ead01-192">There is no action item for you to configure user provisioning to Qualtrics.</span></span> <span data-ttu-id="ead01-193">When an assigned user tries to log into Qualtrics using the access panel, Qualtrics checks whether the user exists.</span><span class="sxs-lookup"><span data-stu-id="ead01-193">When an assigned user tries to log into Qualtrics using the access panel, Qualtrics checks whether the user exists.</span></span>  

<span data-ttu-id="ead01-194">If there is no user account available yet, it is automatically created by Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="ead01-194">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ead01-195">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ead01-195">Assign the Azure AD test user</span></span>

<span data-ttu-id="ead01-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="ead01-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Qualtrics.</span></span>

![Assign the user role][200] 

<span data-ttu-id="ead01-198">**To assign Britta Simon to Qualtrics, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ead01-198">**To assign Britta Simon to Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="ead01-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ead01-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="ead01-201">In the applications list, select **Qualtrics**.</span><span class="sxs-lookup"><span data-stu-id="ead01-201">In the applications list, select **Qualtrics**.</span></span>

    ![The Qualtrics link in the Applications list](./media/qualtrics-tutorial/tutorial_qualtrics_app.png)  

1. <span data-ttu-id="ead01-203">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="ead01-203">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="ead01-205">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="ead01-205">Click **Add** button.</span></span> <span data-ttu-id="ead01-206">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ead01-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="ead01-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="ead01-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="ead01-209">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="ead01-209">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="ead01-210">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ead01-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ead01-211">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="ead01-211">Test single sign-on</span></span>

<span data-ttu-id="ead01-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ead01-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ead01-213">When you click the Qualtrics tile in the Access Panel, you should get automatically signed-on to your Qualtrics application.</span><span class="sxs-lookup"><span data-stu-id="ead01-213">When you click the Qualtrics tile in the Access Panel, you should get automatically signed-on to your Qualtrics application.</span></span>
<span data-ttu-id="ead01-214">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ead01-214">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ead01-215">Additional resources</span><span class="sxs-lookup"><span data-stu-id="ead01-215">Additional resources</span></span>

* [<span data-ttu-id="ead01-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ead01-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="ead01-217">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ead01-217">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/qualtrics-tutorial/tutorial_general_01.png
[2]: ./media/qualtrics-tutorial/tutorial_general_02.png
[3]: ./media/qualtrics-tutorial/tutorial_general_03.png
[4]: ./media/qualtrics-tutorial/tutorial_general_04.png

[100]: ./media/qualtrics-tutorial/tutorial_general_100.png

[200]: ./media/qualtrics-tutorial/tutorial_general_200.png
[201]: ./media/qualtrics-tutorial/tutorial_general_201.png
[202]: ./media/qualtrics-tutorial/tutorial_general_202.png
[203]: ./media/qualtrics-tutorial/tutorial_general_203.png

