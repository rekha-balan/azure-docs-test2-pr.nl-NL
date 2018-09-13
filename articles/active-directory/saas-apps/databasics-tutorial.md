---
title: 'Tutorial: Azure Active Directory integration with DATABASICS | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and DATABASICS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: a37ded45-84c8-4e88-8d9b-c5b9443eb0d4
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/08/2017
ms.author: jeedes
ms.openlocfilehash: 3b177b4e4e6ef66c03ef6c868dcfde9a5277c36d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866143"
---
# <a name="tutorial-azure-active-directory-integration-with-databasics"></a><span data-ttu-id="1a509-103">Tutorial: Azure Active Directory integration with DATABASICS</span><span class="sxs-lookup"><span data-stu-id="1a509-103">Tutorial: Azure Active Directory integration with DATABASICS</span></span>

<span data-ttu-id="1a509-104">In this tutorial, you learn how to integrate DATABASICS with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1a509-104">In this tutorial, you learn how to integrate DATABASICS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1a509-105">Integrating DATABASICS with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1a509-105">Integrating DATABASICS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1a509-106">You can control in Azure AD who has access to DATABASICS.</span><span class="sxs-lookup"><span data-stu-id="1a509-106">You can control in Azure AD who has access to DATABASICS.</span></span>
- <span data-ttu-id="1a509-107">You can enable your users to automatically get signed-on to DATABASICS (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="1a509-107">You can enable your users to automatically get signed-on to DATABASICS (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="1a509-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1a509-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="1a509-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="1a509-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a509-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1a509-110">Prerequisites</span></span>

<span data-ttu-id="1a509-111">To configure Azure AD integration with DATABASICS, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1a509-111">To configure Azure AD integration with DATABASICS, you need the following items:</span></span>

- <span data-ttu-id="1a509-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1a509-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1a509-113">A DATABASICS single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1a509-113">A DATABASICS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1a509-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1a509-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1a509-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1a509-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1a509-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="1a509-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1a509-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1a509-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1a509-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="1a509-118">Scenario description</span></span>
<span data-ttu-id="1a509-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1a509-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1a509-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1a509-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1a509-121">Adding DATABASICS from the gallery</span><span class="sxs-lookup"><span data-stu-id="1a509-121">Adding DATABASICS from the gallery</span></span>
1. <span data-ttu-id="1a509-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1a509-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-databasics-from-the-gallery"></a><span data-ttu-id="1a509-123">Adding DATABASICS from the gallery</span><span class="sxs-lookup"><span data-stu-id="1a509-123">Adding DATABASICS from the gallery</span></span>
<span data-ttu-id="1a509-124">To configure the integration of DATABASICS into Azure AD, you need to add DATABASICS from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1a509-124">To configure the integration of DATABASICS into Azure AD, you need to add DATABASICS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1a509-125">**To add DATABASICS from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1a509-125">**To add DATABASICS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1a509-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="1a509-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="1a509-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="1a509-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1a509-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1a509-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="1a509-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="1a509-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="1a509-133">In the search box, type **DATABASICS**, select **DATABASICS** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="1a509-133">In the search box, type **DATABASICS**, select **DATABASICS** from result panel then click **Add** button to add the application.</span></span>

    ![DATABASICS in the results list](./media/databasics-tutorial/tutorial_databasics_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1a509-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1a509-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1a509-136">In this section, you configure and test Azure AD single sign-on with DATABASICS based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1a509-136">In this section, you configure and test Azure AD single sign-on with DATABASICS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1a509-137">For single sign-on to work, Azure AD needs to know what the counterpart user in DATABASICS is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a509-137">For single sign-on to work, Azure AD needs to know what the counterpart user in DATABASICS is to a user in Azure AD.</span></span> <span data-ttu-id="1a509-138">In other words, a link relationship between an Azure AD user and the related user in DATABASICS needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1a509-138">In other words, a link relationship between an Azure AD user and the related user in DATABASICS needs to be established.</span></span>

<span data-ttu-id="1a509-139">In DATABASICS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="1a509-139">In DATABASICS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1a509-140">To configure and test Azure AD single sign-on with DATABASICS, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1a509-140">To configure and test Azure AD single sign-on with DATABASICS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1a509-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1a509-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="1a509-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1a509-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="1a509-143">**[Create a DATABASICS test user](#create-a-databasics-test-user)** - to have a counterpart of Britta Simon in DATABASICS that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="1a509-143">**[Create a DATABASICS test user](#create-a-databasics-test-user)** - to have a counterpart of Britta Simon in DATABASICS that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="1a509-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1a509-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="1a509-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1a509-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1a509-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1a509-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1a509-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DATABASICS application.</span><span class="sxs-lookup"><span data-stu-id="1a509-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DATABASICS application.</span></span>

<span data-ttu-id="1a509-148">**To configure Azure AD single sign-on with DATABASICS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1a509-148">**To configure Azure AD single sign-on with DATABASICS, perform the following steps:**</span></span>

1. <span data-ttu-id="1a509-149">In the Azure portal, on the **DATABASICS** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1a509-149">In the Azure portal, on the **DATABASICS** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="1a509-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1a509-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/databasics-tutorial/tutorial_databasics_samlbase.png)

1. <span data-ttu-id="1a509-153">On the **DATABASICS Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1a509-153">On the **DATABASICS Domain and URLs** section, perform the following steps:</span></span>

    ![DATABASICS Domain and URLs single sign-on information](./media/databasics-tutorial/tutorial_databasics_url.png)

    <span data-ttu-id="1a509-155">a.</span><span class="sxs-lookup"><span data-stu-id="1a509-155">a.</span></span> <span data-ttu-id="1a509-156">In the **Identifier** textbox, type the value: `DATA-BASICS_SP`</span><span class="sxs-lookup"><span data-stu-id="1a509-156">In the **Identifier** textbox, type the value: `DATA-BASICS_SP`</span></span>
    
    <span data-ttu-id="1a509-157">b.</span><span class="sxs-lookup"><span data-stu-id="1a509-157">b.</span></span> <span data-ttu-id="1a509-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sitenumber>.data-basics.net/<clientname>/saml_sso.jsp`</span><span class="sxs-lookup"><span data-stu-id="1a509-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sitenumber>.data-basics.net/<clientname>/saml_sso.jsp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1a509-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="1a509-159">These values are not real.</span></span> <span data-ttu-id="1a509-160">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="1a509-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1a509-161">Contact [DATABASICS Client support team](https://www.data-basics.com/support/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="1a509-161">Contact [DATABASICS Client support team](https://www.data-basics.com/support/) to get these values.</span></span>

1. <span data-ttu-id="1a509-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="1a509-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/databasics-tutorial/tutorial_databasics_certificate.png) 

1. <span data-ttu-id="1a509-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="1a509-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/databasics-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="1a509-166">To configure single sign-on on the DATABASICS side, please complete the form using the URL below.</span><span class="sxs-lookup"><span data-stu-id="1a509-166">To configure single sign-on on the DATABASICS side, please complete the form using the URL below.</span></span> <span data-ttu-id="1a509-167">Once the form is submitted, the [DATABASICS Client support team](https://www.data-basics.com/support/) will contact you.</span><span class="sxs-lookup"><span data-stu-id="1a509-167">Once the form is submitted, the [DATABASICS Client support team](https://www.data-basics.com/support/) will contact you.</span></span>
    
    [https://www.data-basics.com/support/submit-sso-onboarding-request/](https://www.data-basics.com/support/submit-sso-onboarding-request/)


> [!TIP]
> <span data-ttu-id="1a509-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="1a509-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1a509-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="1a509-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1a509-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1a509-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1a509-171">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1a509-171">Create an Azure AD test user</span></span>

<span data-ttu-id="1a509-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1a509-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="1a509-174">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1a509-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1a509-175">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="1a509-175">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/databasics-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="1a509-177">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="1a509-177">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/databasics-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="1a509-179">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="1a509-179">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/databasics-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="1a509-181">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1a509-181">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/databasics-tutorial/create_aaduser_04.png)

    <span data-ttu-id="1a509-183">a.</span><span class="sxs-lookup"><span data-stu-id="1a509-183">a.</span></span> <span data-ttu-id="1a509-184">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1a509-184">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1a509-185">b.</span><span class="sxs-lookup"><span data-stu-id="1a509-185">b.</span></span> <span data-ttu-id="1a509-186">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1a509-186">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="1a509-187">c.</span><span class="sxs-lookup"><span data-stu-id="1a509-187">c.</span></span> <span data-ttu-id="1a509-188">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="1a509-188">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="1a509-189">d.</span><span class="sxs-lookup"><span data-stu-id="1a509-189">d.</span></span> <span data-ttu-id="1a509-190">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1a509-190">Click **Create**.</span></span>
 
### <a name="create-a-databasics-test-user"></a><span data-ttu-id="1a509-191">Create a DATABASICS test user</span><span class="sxs-lookup"><span data-stu-id="1a509-191">Create a DATABASICS test user</span></span>

<span data-ttu-id="1a509-192">In this section, you create a user called Britta Simon in DATABASICS.</span><span class="sxs-lookup"><span data-stu-id="1a509-192">In this section, you create a user called Britta Simon in DATABASICS.</span></span> <span data-ttu-id="1a509-193">Work with [DATABASICS support team](https://www.data-basics.com/support/) to add the users in the DATABASICS platform.</span><span class="sxs-lookup"><span data-stu-id="1a509-193">Work with [DATABASICS support team](https://www.data-basics.com/support/) to add the users in the DATABASICS platform.</span></span> <span data-ttu-id="1a509-194">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1a509-194">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1a509-195">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1a509-195">Assign the Azure AD test user</span></span>

<span data-ttu-id="1a509-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to DATABASICS.</span><span class="sxs-lookup"><span data-stu-id="1a509-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to DATABASICS.</span></span>

![Assign the user role][200] 

<span data-ttu-id="1a509-198">**To assign Britta Simon to DATABASICS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1a509-198">**To assign Britta Simon to DATABASICS, perform the following steps:**</span></span>

1. <span data-ttu-id="1a509-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1a509-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="1a509-201">In the applications list, select **DATABASICS**.</span><span class="sxs-lookup"><span data-stu-id="1a509-201">In the applications list, select **DATABASICS**.</span></span>

    ![The DATABASICS link in the Applications list](./media/databasics-tutorial/tutorial_databasics_app.png)  

1. <span data-ttu-id="1a509-203">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="1a509-203">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="1a509-205">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="1a509-205">Click **Add** button.</span></span> <span data-ttu-id="1a509-206">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1a509-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="1a509-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="1a509-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="1a509-209">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="1a509-209">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="1a509-210">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1a509-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1a509-211">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="1a509-211">Test single sign-on</span></span>

<span data-ttu-id="1a509-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1a509-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1a509-213">When you click the DATABASICS tile in the Access Panel, you should get automatically signed-on to your DATABASICS application.</span><span class="sxs-lookup"><span data-stu-id="1a509-213">When you click the DATABASICS tile in the Access Panel, you should get automatically signed-on to your DATABASICS application.</span></span>
<span data-ttu-id="1a509-214">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1a509-214">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1a509-215">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1a509-215">Additional resources</span></span>

* [<span data-ttu-id="1a509-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a509-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="1a509-217">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1a509-217">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)


<!--Image references-->

[1]: ./media/databasics-tutorial/tutorial_general_01.png
[2]: ./media/databasics-tutorial/tutorial_general_02.png
[3]: ./media/databasics-tutorial/tutorial_general_03.png
[4]: ./media/databasics-tutorial/tutorial_general_04.png

[100]: ./media/databasics-tutorial/tutorial_general_100.png

[200]: ./media/databasics-tutorial/tutorial_general_200.png
[201]: ./media/databasics-tutorial/tutorial_general_201.png
[202]: ./media/databasics-tutorial/tutorial_general_202.png
[203]: ./media/databasics-tutorial/tutorial_general_203.png

