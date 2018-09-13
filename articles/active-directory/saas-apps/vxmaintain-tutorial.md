---
title: 'Tutorial: Azure Active Directory integration with vxMaintain | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and vxMaintain.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2018
ms.author: jeedes
ms.openlocfilehash: 7e444692dfeab5ca14fbd896043cc28e2cbd8717
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869876"
---
# <a name="tutorial-azure-active-directory-integration-with-vxmaintain"></a><span data-ttu-id="49a4c-103">Tutorial: Azure Active Directory integration with vxMaintain</span><span class="sxs-lookup"><span data-stu-id="49a4c-103">Tutorial: Azure Active Directory integration with vxMaintain</span></span>

<span data-ttu-id="49a4c-104">In this tutorial, you learn how to integrate vxMaintain with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="49a4c-104">In this tutorial, you learn how to integrate vxMaintain with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="49a4c-105">This integration provides several important benefits.</span><span class="sxs-lookup"><span data-stu-id="49a4c-105">This integration provides several important benefits.</span></span> <span data-ttu-id="49a4c-106">You can:</span><span class="sxs-lookup"><span data-stu-id="49a4c-106">You can:</span></span>

- <span data-ttu-id="49a4c-107">Control in Azure AD who has access to vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="49a4c-107">Control in Azure AD who has access to vxMaintain.</span></span>
- <span data-ttu-id="49a4c-108">Enable your users to automatically sign in to vxMaintain with single sign-on (SSO) by using their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="49a4c-108">Enable your users to automatically sign in to vxMaintain with single sign-on (SSO) by using their Azure AD accounts.</span></span>
- <span data-ttu-id="49a4c-109">Manage your accounts in one central location: the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="49a4c-109">Manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="49a4c-110">To learn more about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="49a4c-110">To learn more about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49a4c-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="49a4c-111">Prerequisites</span></span>

<span data-ttu-id="49a4c-112">To configure Azure AD integration with vxMaintain, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="49a4c-112">To configure Azure AD integration with vxMaintain, you need the following items:</span></span>

- <span data-ttu-id="49a4c-113">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="49a4c-113">An Azure AD subscription</span></span>
- <span data-ttu-id="49a4c-114">A vxMaintain SSO-enabled subscription</span><span class="sxs-lookup"><span data-stu-id="49a4c-114">A vxMaintain SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="49a4c-115">When you test the steps in this tutorial, we recommend that you do not use a production environment.</span><span class="sxs-lookup"><span data-stu-id="49a4c-115">When you test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="49a4c-116">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="49a4c-116">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="49a4c-117">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="49a4c-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="49a4c-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="49a4c-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="49a4c-119">Scenario description</span><span class="sxs-lookup"><span data-stu-id="49a4c-119">Scenario description</span></span>
<span data-ttu-id="49a4c-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="49a4c-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="49a4c-121">The scenario that this tutorial outlines consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="49a4c-121">The scenario that this tutorial outlines consists of two main building blocks:</span></span>

* <span data-ttu-id="49a4c-122">Adding vxMaintain from the gallery</span><span class="sxs-lookup"><span data-stu-id="49a4c-122">Adding vxMaintain from the gallery</span></span>
* <span data-ttu-id="49a4c-123">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="49a4c-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-vxmaintain-from-the-gallery"></a><span data-ttu-id="49a4c-124">Add vxMaintain from the gallery</span><span class="sxs-lookup"><span data-stu-id="49a4c-124">Add vxMaintain from the gallery</span></span>
<span data-ttu-id="49a4c-125">To configure the integration of vxMaintain with Azure AD, you need to add vxMaintain from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="49a4c-125">To configure the integration of vxMaintain with Azure AD, you need to add vxMaintain from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="49a4c-126">To add vxMaintain from the gallery, do the following:</span><span class="sxs-lookup"><span data-stu-id="49a4c-126">To add vxMaintain from the gallery, do the following:</span></span>

1. <span data-ttu-id="49a4c-127">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="49a4c-127">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** button.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="49a4c-129">Select **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="49a4c-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![The "Enterprise applications" pane][2]
    
1. <span data-ttu-id="49a4c-131">To add an application, in the **All applications** dialog box, select **New application**.</span><span class="sxs-lookup"><span data-stu-id="49a4c-131">To add an application, in the **All applications** dialog box, select **New application**.</span></span>

    ![The "New application" button][3]

1. <span data-ttu-id="49a4c-133">In the search box, type **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="49a4c-133">In the search box, type **vxMaintain**.</span></span>

    ![The "Single Sign-on Mode" drop-down list](./media/vxmaintain-tutorial/tutorial_vxmaintain_search.png)

1. <span data-ttu-id="49a4c-135">In the results list, select **vxMaintain**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="49a4c-135">In the results list, select **vxMaintain**, and then select **Add**.</span></span>

    ![The vxMaintain link](./media/vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="49a4c-137">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="49a4c-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="49a4c-138">In this section, you configure and test Azure AD SSO by using vxMaintain, based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="49a4c-138">In this section, you configure and test Azure AD SSO by using vxMaintain, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="49a4c-139">For SSO to work, Azure AD needs to know the vxMaintain counterpart to the Azure AD user.</span><span class="sxs-lookup"><span data-stu-id="49a4c-139">For SSO to work, Azure AD needs to know the vxMaintain counterpart to the Azure AD user.</span></span> <span data-ttu-id="49a4c-140">That is, you must establish a link relationship between the Azure AD user and the corresponding vxMaintain user.</span><span class="sxs-lookup"><span data-stu-id="49a4c-140">That is, you must establish a link relationship between the Azure AD user and the corresponding vxMaintain user.</span></span>

<span data-ttu-id="49a4c-141">To establish the link relationship, assign the vxMaintain **user name** value as the Azure AD **Username** value.</span><span class="sxs-lookup"><span data-stu-id="49a4c-141">To establish the link relationship, assign the vxMaintain **user name** value as the Azure AD **Username** value.</span></span>

<span data-ttu-id="49a4c-142">To configure and test Azure AD SSO by using vxMaintain, complete the following building blocks.</span><span class="sxs-lookup"><span data-stu-id="49a4c-142">To configure and test Azure AD SSO by using vxMaintain, complete the following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="49a4c-143">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="49a4c-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="49a4c-144">In this section, you can both enable Azure AD SSO in the Azure portal and configure SSO in your vxMaintain application by doing the following:</span><span class="sxs-lookup"><span data-stu-id="49a4c-144">In this section, you can both enable Azure AD SSO in the Azure portal and configure SSO in your vxMaintain application by doing the following:</span></span>

1. <span data-ttu-id="49a4c-145">In the Azure portal, on the **vxMaintain** application integration page, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="49a4c-145">In the Azure portal, on the **vxMaintain** application integration page, select **Single sign-on**.</span></span>

    ![The "Single sign-on" command][4]

1. <span data-ttu-id="49a4c-147">To enable SSO, in the **Single Sign-on Mode** drop-down list, select **SAML-based Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="49a4c-147">To enable SSO, in the **Single Sign-on Mode** drop-down list, select **SAML-based Sign-on**.</span></span>
 
    ![The "SAML-based Sign-on" command](./media/vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

1. <span data-ttu-id="49a4c-149">Under **vxMaintain Domain and URLs**, do the following:</span><span class="sxs-lookup"><span data-stu-id="49a4c-149">Under **vxMaintain Domain and URLs**, do the following:</span></span>

    ![The vxMaintain Domain and URLs section](./media/vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    <span data-ttu-id="49a4c-151">a.</span><span class="sxs-lookup"><span data-stu-id="49a4c-151">a.</span></span> <span data-ttu-id="49a4c-152">In the **Identifier** box, type a URL that has the following syntax: `https://<company name>.verisae.com`</span><span class="sxs-lookup"><span data-stu-id="49a4c-152">In the **Identifier** box, type a URL that has the following syntax: `https://<company name>.verisae.com`</span></span>

    <span data-ttu-id="49a4c-153">b.</span><span class="sxs-lookup"><span data-stu-id="49a4c-153">b.</span></span> <span data-ttu-id="49a4c-154">In the **Reply URL** box, type a URL that has the following syntax: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span><span class="sxs-lookup"><span data-stu-id="49a4c-154">In the **Reply URL** box, type a URL that has the following syntax: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="49a4c-155">The preceding values are not real.</span><span class="sxs-lookup"><span data-stu-id="49a4c-155">The preceding values are not real.</span></span> <span data-ttu-id="49a4c-156">Update them with the actual identifier and reply URL.</span><span class="sxs-lookup"><span data-stu-id="49a4c-156">Update them with the actual identifier and reply URL.</span></span> <span data-ttu-id="49a4c-157">To obtain the values, contact the [vxMaintain support team](https://www.hubspot.com/company/contact).</span><span class="sxs-lookup"><span data-stu-id="49a4c-157">To obtain the values, contact the [vxMaintain support team](https://www.hubspot.com/company/contact).</span></span>
 
1. <span data-ttu-id="49a4c-158">Under **SAML Signing Certificate**, select **Metadata XML**, and then save the metadata file to your computer.</span><span class="sxs-lookup"><span data-stu-id="49a4c-158">Under **SAML Signing Certificate**, select **Metadata XML**, and then save the metadata file to your computer.</span></span>

    ![The "SAML Signing Certificate" section](./media/vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

1. <span data-ttu-id="49a4c-160">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="49a4c-160">Select **Save**.</span></span>

    ![The Save button](./media/vxmaintain-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="49a4c-162">To configure **vxMaintain** SSO, send the downloaded **Metadata XML** file to the [vxMaintain support team](https://www.hubspot.com/company/contact).</span><span class="sxs-lookup"><span data-stu-id="49a4c-162">To configure **vxMaintain** SSO, send the downloaded **Metadata XML** file to the [vxMaintain support team](https://www.hubspot.com/company/contact).</span></span>

> [!TIP]
> <span data-ttu-id="49a4c-163">As you set up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="49a4c-163">As you set up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="49a4c-164">After you add the app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab, and then access the embedded documentation from the **Configuration** section.</span><span class="sxs-lookup"><span data-stu-id="49a4c-164">After you add the app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab, and then access the embedded documentation from the **Configuration** section.</span></span> 
>
><span data-ttu-id="49a4c-165">To learn more about the embedded documentation feature, see [Managing single sign-on for enterprise apps](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="49a4c-165">To learn more about the embedded documentation feature, see [Managing single sign-on for enterprise apps](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="49a4c-166">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="49a4c-166">Create an Azure AD test user</span></span>
<span data-ttu-id="49a4c-167">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span><span class="sxs-lookup"><span data-stu-id="49a4c-167">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span></span>

![The Azure AD test user][100]

1. <span data-ttu-id="49a4c-169">In the **Azure portal**, in the left pane, select the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="49a4c-169">In the **Azure portal**, in the left pane, select the **Azure Active Directory** button.</span></span>

    ![The "Azure Active Directory" button](./media/vxmaintain-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="49a4c-171">To display a list of users, go to **Users and groups** > **All users**.</span><span class="sxs-lookup"><span data-stu-id="49a4c-171">To display a list of users, go to **Users and groups** > **All users**.</span></span>
    
    <span data-ttu-id="49a4c-172">![The "All users" link](./media/vxmaintain-tutorial/create_aaduser_02.png)</span><span class="sxs-lookup"><span data-stu-id="49a4c-172">![The "All users" link](./media/vxmaintain-tutorial/create_aaduser_02.png)</span></span>  
    <span data-ttu-id="49a4c-173">The **All users** dialog box opens.</span><span class="sxs-lookup"><span data-stu-id="49a4c-173">The **All users** dialog box opens.</span></span> 

1. <span data-ttu-id="49a4c-174">To open the **User** dialog box, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="49a4c-174">To open the **User** dialog box, select **Add**.</span></span>
 
    ![The Add button](./media/vxmaintain-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="49a4c-176">In the **User** dialog box, do the following:</span><span class="sxs-lookup"><span data-stu-id="49a4c-176">In the **User** dialog box, do the following:</span></span>
 
    ![The User dialog box](./media/vxmaintain-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="49a4c-178">a.</span><span class="sxs-lookup"><span data-stu-id="49a4c-178">a.</span></span> <span data-ttu-id="49a4c-179">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="49a4c-179">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="49a4c-180">b.</span><span class="sxs-lookup"><span data-stu-id="49a4c-180">b.</span></span> <span data-ttu-id="49a4c-181">In the **User name** box, type the email address of test user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="49a4c-181">In the **User name** box, type the email address of test user Britta Simon.</span></span>

    <span data-ttu-id="49a4c-182">c.</span><span class="sxs-lookup"><span data-stu-id="49a4c-182">c.</span></span> <span data-ttu-id="49a4c-183">Select the **Show Password** check box, and then note the value that was generated in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="49a4c-183">Select the **Show Password** check box, and then note the value that was generated in the **Password** box.</span></span>

    <span data-ttu-id="49a4c-184">d.</span><span class="sxs-lookup"><span data-stu-id="49a4c-184">d.</span></span> <span data-ttu-id="49a4c-185">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="49a4c-185">Select **Create**.</span></span>
 
### <a name="create-a-vxmaintain-test-user"></a><span data-ttu-id="49a4c-186">Create a vxMaintain test user</span><span class="sxs-lookup"><span data-stu-id="49a4c-186">Create a vxMaintain test user</span></span>

<span data-ttu-id="49a4c-187">In this section, you create test user Britta Simon in vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="49a4c-187">In this section, you create test user Britta Simon in vxMaintain.</span></span> <span data-ttu-id="49a4c-188">To add users in the vxMaintain platform, work with the [vxMaintain support team](https://www.hubspot.com/company/contact).</span><span class="sxs-lookup"><span data-stu-id="49a4c-188">To add users in the vxMaintain platform, work with the [vxMaintain support team](https://www.hubspot.com/company/contact).</span></span> <span data-ttu-id="49a4c-189">Before you use SSO, create and activate the users.</span><span class="sxs-lookup"><span data-stu-id="49a4c-189">Before you use SSO, create and activate the users.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="49a4c-190">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="49a4c-190">Assign the Azure AD test user</span></span>

<span data-ttu-id="49a4c-191">In this section, you enable test user Britta Simon to use Azure SSO by granting access to vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="49a4c-191">In this section, you enable test user Britta Simon to use Azure SSO by granting access to vxMaintain.</span></span> <span data-ttu-id="49a4c-192">To do so, do the following:</span><span class="sxs-lookup"><span data-stu-id="49a4c-192">To do so, do the following:</span></span>

![Test user in the Display Name list][200] 

1. <span data-ttu-id="49a4c-194">In the Azure portal **Applications** view, go to **Directory** view > **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="49a4c-194">In the Azure portal **Applications** view, go to **Directory** view > **Enterprise applications** > **All applications**.</span></span>

    ![The "All applications" link][201] 

1. <span data-ttu-id="49a4c-196">In the **Applications** list, select **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="49a4c-196">In the **Applications** list, select **vxMaintain**.</span></span>

    ![The vxMaintain link](./media/vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

1. <span data-ttu-id="49a4c-198">In the left pane, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="49a4c-198">In the left pane, select **Users and groups**.</span></span>

    ![The "Users and groups" link][202] 

1. <span data-ttu-id="49a4c-200">Select **Add** and then, in the **Add Assignment** pane, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="49a4c-200">Select **Add** and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![The "Users and groups" link][203]

1. <span data-ttu-id="49a4c-202">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**, and then select the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="49a4c-202">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**, and then select the **Select** button.</span></span>

1. <span data-ttu-id="49a4c-203">In the **Add Assignment** dialog box, select **Assign**.</span><span class="sxs-lookup"><span data-stu-id="49a4c-203">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-your-azure-ad-single-sign-on"></a><span data-ttu-id="49a4c-204">Test your Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="49a4c-204">Test your Azure AD single sign-on</span></span>

<span data-ttu-id="49a4c-205">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="49a4c-205">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="49a4c-206">Selecting the **vxMaintain** tile in the Access Panel should sign you in to your vxMaintain application automatically.</span><span class="sxs-lookup"><span data-stu-id="49a4c-206">Selecting the **vxMaintain** tile in the Access Panel should sign you in to your vxMaintain application automatically.</span></span>

<span data-ttu-id="49a4c-207">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="49a4c-207">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="49a4c-208">Next steps</span><span class="sxs-lookup"><span data-stu-id="49a4c-208">Next steps</span></span>

* [<span data-ttu-id="49a4c-209">List of tutorials on integrating SaaS apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49a4c-209">List of tutorials on integrating SaaS apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="49a4c-210">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="49a4c-210">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/vxmaintain-tutorial/tutorial_general_203.png

