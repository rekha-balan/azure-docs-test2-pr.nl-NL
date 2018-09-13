---
title: 'Tutorial: Azure Active Directory integration with Sedgwick CMS | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Sedgwick CMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 957931e0-e426-47e7-9904-3ed98d3f504c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: jeedes
ms.openlocfilehash: ff9f3186602b9047e53fb78edbf52c2c0d9ee574
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967793"
---
# <a name="tutorial-azure-active-directory-integration-with-sedgwick-cms"></a><span data-ttu-id="580fb-103">Tutorial: Azure Active Directory integration with Sedgwick CMS</span><span class="sxs-lookup"><span data-stu-id="580fb-103">Tutorial: Azure Active Directory integration with Sedgwick CMS</span></span>

<span data-ttu-id="580fb-104">In this tutorial, you learn how to integrate Sedgwick CMS with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="580fb-104">In this tutorial, you learn how to integrate Sedgwick CMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="580fb-105">Integrating Sedgwick CMS with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="580fb-105">Integrating Sedgwick CMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="580fb-106">You can control in Azure AD who has access to Sedgwick CMS.</span><span class="sxs-lookup"><span data-stu-id="580fb-106">You can control in Azure AD who has access to Sedgwick CMS.</span></span>
- <span data-ttu-id="580fb-107">You can enable your users to automatically get signed-on to Sedgwick CMS (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="580fb-107">You can enable your users to automatically get signed-on to Sedgwick CMS (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="580fb-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="580fb-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="580fb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="580fb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="580fb-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="580fb-110">Prerequisites</span></span>

<span data-ttu-id="580fb-111">To configure Azure AD integration with Sedgwick CMS, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="580fb-111">To configure Azure AD integration with Sedgwick CMS, you need the following items:</span></span>

- <span data-ttu-id="580fb-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="580fb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="580fb-113">A Sedgwick CMS single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="580fb-113">A Sedgwick CMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="580fb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="580fb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="580fb-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="580fb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="580fb-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="580fb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="580fb-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="580fb-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="580fb-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="580fb-118">Scenario description</span></span>
<span data-ttu-id="580fb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="580fb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="580fb-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="580fb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="580fb-121">Adding Sedgwick CMS from the gallery</span><span class="sxs-lookup"><span data-stu-id="580fb-121">Adding Sedgwick CMS from the gallery</span></span>
1. <span data-ttu-id="580fb-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="580fb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sedgwick-cms-from-the-gallery"></a><span data-ttu-id="580fb-123">Adding Sedgwick CMS from the gallery</span><span class="sxs-lookup"><span data-stu-id="580fb-123">Adding Sedgwick CMS from the gallery</span></span>
<span data-ttu-id="580fb-124">To configure the integration of Sedgwick CMS into Azure AD, you need to add Sedgwick CMS from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="580fb-124">To configure the integration of Sedgwick CMS into Azure AD, you need to add Sedgwick CMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="580fb-125">**To add Sedgwick CMS from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="580fb-125">**To add Sedgwick CMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="580fb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="580fb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="580fb-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="580fb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="580fb-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="580fb-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="580fb-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="580fb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="580fb-133">In the search box, type **Sedgwick CMS**, select **Sedgwick CMS** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="580fb-133">In the search box, type **Sedgwick CMS**, select **Sedgwick CMS** from result panel then click **Add** button to add the application.</span></span>

    ![Sedgwick CMS in the results list](./media/sedgwickcms-tutorial/tutorial_sedgwickcms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="580fb-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="580fb-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="580fb-136">In this section, you configure and test Azure AD single sign-on with Sedgwick CMS based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="580fb-136">In this section, you configure and test Azure AD single sign-on with Sedgwick CMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="580fb-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Sedgwick CMS is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="580fb-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Sedgwick CMS is to a user in Azure AD.</span></span> <span data-ttu-id="580fb-138">In other words, a link relationship between an Azure AD user and the related user in Sedgwick CMS needs to be established.</span><span class="sxs-lookup"><span data-stu-id="580fb-138">In other words, a link relationship between an Azure AD user and the related user in Sedgwick CMS needs to be established.</span></span>

<span data-ttu-id="580fb-139">In Sedgwick CMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="580fb-139">In Sedgwick CMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="580fb-140">To configure and test Azure AD single sign-on with Sedgwick CMS, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="580fb-140">To configure and test Azure AD single sign-on with Sedgwick CMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="580fb-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="580fb-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="580fb-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="580fb-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="580fb-143">**[Create a Sedgwick CMS test user](#create-a-sedgwick-cms-test-user)** - to have a counterpart of Britta Simon in Sedgwick CMS that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="580fb-143">**[Create a Sedgwick CMS test user](#create-a-sedgwick-cms-test-user)** - to have a counterpart of Britta Simon in Sedgwick CMS that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="580fb-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="580fb-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="580fb-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="580fb-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="580fb-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="580fb-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="580fb-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sedgwick CMS application.</span><span class="sxs-lookup"><span data-stu-id="580fb-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sedgwick CMS application.</span></span>

<span data-ttu-id="580fb-148">**To configure Azure AD single sign-on with Sedgwick CMS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="580fb-148">**To configure Azure AD single sign-on with Sedgwick CMS, perform the following steps:**</span></span>

1. <span data-ttu-id="580fb-149">In the Azure portal, on the **Sedgwick CMS** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="580fb-149">In the Azure portal, on the **Sedgwick CMS** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="580fb-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="580fb-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/sedgwickcms-tutorial/tutorial_sedgwickcms_samlbase.png)

1. <span data-ttu-id="580fb-153">On the **Sedgwick CMS Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="580fb-153">On the **Sedgwick CMS Domain and URLs** section, perform the following steps:</span></span>

    ![Sedgwick CMS Domain and URLs single sign-on information](./media/sedgwickcms-tutorial/tutorial_sedgwickcms_url.png)

    <span data-ttu-id="580fb-155">a.</span><span class="sxs-lookup"><span data-stu-id="580fb-155">a.</span></span> <span data-ttu-id="580fb-156">In the **Identifier** textbox, type the URL:</span><span class="sxs-lookup"><span data-stu-id="580fb-156">In the **Identifier** textbox, type the URL:</span></span> 
    | |
    |--|
    | `expresspreview.sedgwickcms.net/voe/sso` |
    | `claimlookup.com/Voe/sso` |

    <span data-ttu-id="580fb-157">b.</span><span class="sxs-lookup"><span data-stu-id="580fb-157">b.</span></span> <span data-ttu-id="580fb-158">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="580fb-158">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.sedgwickcms.net/voe/sso` |
    | `https://claimlookup.com/Voe/sso` |

    > [!NOTE] 
    > <span data-ttu-id="580fb-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="580fb-159">These values are not real.</span></span> <span data-ttu-id="580fb-160">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="580fb-160">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="580fb-161">Contact [Sedgwick CMS support team](https://www.sedgwick.com/help) to get these values.</span><span class="sxs-lookup"><span data-stu-id="580fb-161">Contact [Sedgwick CMS support team](https://www.sedgwick.com/help) to get these values.</span></span>
 

1. <span data-ttu-id="580fb-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="580fb-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/sedgwickcms-tutorial/tutorial_sedgwickcms_certificate.png) 

1. <span data-ttu-id="580fb-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="580fb-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/sedgwickcms-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="580fb-166">To configure single sign-on on **Sedgwick CMS** side, you need to send the downloaded **Metadata XML** to [Sedgwick CMS support team](https://www.sedgwick.com/contact/Pages/contactform.aspx).</span><span class="sxs-lookup"><span data-stu-id="580fb-166">To configure single sign-on on **Sedgwick CMS** side, you need to send the downloaded **Metadata XML** to [Sedgwick CMS support team](https://www.sedgwick.com/contact/Pages/contactform.aspx).</span></span> <span data-ttu-id="580fb-167">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="580fb-167">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="580fb-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="580fb-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="580fb-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="580fb-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="580fb-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="580fb-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="580fb-171">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="580fb-171">Create an Azure AD test user</span></span>

<span data-ttu-id="580fb-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="580fb-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="580fb-174">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="580fb-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="580fb-175">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="580fb-175">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/sedgwickcms-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="580fb-177">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="580fb-177">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/sedgwickcms-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="580fb-179">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="580fb-179">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/sedgwickcms-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="580fb-181">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="580fb-181">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/sedgwickcms-tutorial/create_aaduser_04.png)

    <span data-ttu-id="580fb-183">a.</span><span class="sxs-lookup"><span data-stu-id="580fb-183">a.</span></span> <span data-ttu-id="580fb-184">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="580fb-184">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="580fb-185">b.</span><span class="sxs-lookup"><span data-stu-id="580fb-185">b.</span></span> <span data-ttu-id="580fb-186">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="580fb-186">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="580fb-187">c.</span><span class="sxs-lookup"><span data-stu-id="580fb-187">c.</span></span> <span data-ttu-id="580fb-188">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="580fb-188">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="580fb-189">d.</span><span class="sxs-lookup"><span data-stu-id="580fb-189">d.</span></span> <span data-ttu-id="580fb-190">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="580fb-190">Click **Create**.</span></span>
  
### <a name="create-a-sedgwick-cms-test-user"></a><span data-ttu-id="580fb-191">Create a Sedgwick CMS test user</span><span class="sxs-lookup"><span data-stu-id="580fb-191">Create a Sedgwick CMS test user</span></span>

<span data-ttu-id="580fb-192">In this section, you create a user called Britta Simon in Sedgwick CMS.</span><span class="sxs-lookup"><span data-stu-id="580fb-192">In this section, you create a user called Britta Simon in Sedgwick CMS.</span></span> <span data-ttu-id="580fb-193">Work with [Sedgwick CMS support team](https://www.sedgwick.com/contact/Pages/contactform.aspx) to add the users in the Sedgwick CMS platform.</span><span class="sxs-lookup"><span data-stu-id="580fb-193">Work with [Sedgwick CMS support team](https://www.sedgwick.com/contact/Pages/contactform.aspx) to add the users in the Sedgwick CMS platform.</span></span> <span data-ttu-id="580fb-194">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="580fb-194">Users must be created and activated before you use single sign-on.</span></span>  

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="580fb-195">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="580fb-195">Assign the Azure AD test user</span></span>

<span data-ttu-id="580fb-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sedgwick CMS.</span><span class="sxs-lookup"><span data-stu-id="580fb-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sedgwick CMS.</span></span>

![Assign the user role][200] 

<span data-ttu-id="580fb-198">**To assign Britta Simon to Sedgwick CMS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="580fb-198">**To assign Britta Simon to Sedgwick CMS, perform the following steps:**</span></span>

1. <span data-ttu-id="580fb-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="580fb-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="580fb-201">In the applications list, select **Sedgwick CMS**.</span><span class="sxs-lookup"><span data-stu-id="580fb-201">In the applications list, select **Sedgwick CMS**.</span></span>

    ![The Sedgwick CMS link in the Applications list](./media/sedgwickcms-tutorial/tutorial_sedgwickcms_app.png)  

1. <span data-ttu-id="580fb-203">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="580fb-203">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="580fb-205">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="580fb-205">Click **Add** button.</span></span> <span data-ttu-id="580fb-206">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="580fb-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="580fb-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="580fb-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="580fb-209">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="580fb-209">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="580fb-210">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="580fb-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="580fb-211">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="580fb-211">Test single sign-on</span></span>

<span data-ttu-id="580fb-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="580fb-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="580fb-213">When you click the Sedgwick CMS tile in the Access Panel, you should get automatically signed-on to your Sedgwick CMS application.</span><span class="sxs-lookup"><span data-stu-id="580fb-213">When you click the Sedgwick CMS tile in the Access Panel, you should get automatically signed-on to your Sedgwick CMS application.</span></span>
<span data-ttu-id="580fb-214">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="580fb-214">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="580fb-215">Additional resources</span><span class="sxs-lookup"><span data-stu-id="580fb-215">Additional resources</span></span>

* [<span data-ttu-id="580fb-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="580fb-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="580fb-217">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="580fb-217">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/sedgwickcms-tutorial/tutorial_general_01.png
[2]: ./media/sedgwickcms-tutorial/tutorial_general_02.png
[3]: ./media/sedgwickcms-tutorial/tutorial_general_03.png
[4]: ./media/sedgwickcms-tutorial/tutorial_general_04.png

[100]: ./media/sedgwickcms-tutorial/tutorial_general_100.png

[200]: ./media/sedgwickcms-tutorial/tutorial_general_200.png
[201]: ./media/sedgwickcms-tutorial/tutorial_general_201.png
[202]: ./media/sedgwickcms-tutorial/tutorial_general_202.png
[203]: ./media/sedgwickcms-tutorial/tutorial_general_203.png

