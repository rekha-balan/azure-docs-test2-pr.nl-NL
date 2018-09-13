---
title: 'Tutorial: Azure Active Directory integration with Skills Manager | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Skills Manager.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: dab8debd-3b7b-4656-9bf0-1963ad8fce05
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2017
ms.author: jeedes
ms.openlocfilehash: ee112cef53eec92ec449c66e0c927a78a087a32c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864922"
---
# <a name="tutorial-azure-active-directory-integration-with-skills-manager"></a><span data-ttu-id="9c508-103">Tutorial: Azure Active Directory integration with Skills Manager</span><span class="sxs-lookup"><span data-stu-id="9c508-103">Tutorial: Azure Active Directory integration with Skills Manager</span></span>

<span data-ttu-id="9c508-104">In this tutorial, you learn how to integrate Skills Manager with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9c508-104">In this tutorial, you learn how to integrate Skills Manager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9c508-105">Integrating Skills Manager with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="9c508-105">Integrating Skills Manager with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9c508-106">You can control in Azure AD who has access to Skills Manager.</span><span class="sxs-lookup"><span data-stu-id="9c508-106">You can control in Azure AD who has access to Skills Manager.</span></span>
- <span data-ttu-id="9c508-107">You can enable your users to automatically get signed-on to Skills Manager (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="9c508-107">You can enable your users to automatically get signed-on to Skills Manager (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9c508-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9c508-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="9c508-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="9c508-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c508-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9c508-110">Prerequisites</span></span>

<span data-ttu-id="9c508-111">To configure Azure AD integration with Skills Manager, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="9c508-111">To configure Azure AD integration with Skills Manager, you need the following items:</span></span>

- <span data-ttu-id="9c508-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="9c508-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9c508-113">A Skills Manager single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="9c508-113">A Skills Manager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9c508-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="9c508-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9c508-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="9c508-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9c508-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="9c508-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9c508-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9c508-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9c508-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="9c508-118">Scenario description</span></span>
<span data-ttu-id="9c508-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="9c508-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9c508-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="9c508-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9c508-121">Adding Skills Manager from the gallery</span><span class="sxs-lookup"><span data-stu-id="9c508-121">Adding Skills Manager from the gallery</span></span>
1. <span data-ttu-id="9c508-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9c508-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skills-manager-from-the-gallery"></a><span data-ttu-id="9c508-123">Adding Skills Manager from the gallery</span><span class="sxs-lookup"><span data-stu-id="9c508-123">Adding Skills Manager from the gallery</span></span>
<span data-ttu-id="9c508-124">To configure the integration of Skills Manager into Azure AD, you need to add Skills Manager from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="9c508-124">To configure the integration of Skills Manager into Azure AD, you need to add Skills Manager from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9c508-125">**To add Skills Manager from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9c508-125">**To add Skills Manager from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9c508-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9c508-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="9c508-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="9c508-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9c508-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9c508-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="9c508-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="9c508-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="9c508-133">In the search box, type **Skills Manager**, select **Skills Manager** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="9c508-133">In the search box, type **Skills Manager**, select **Skills Manager** from result panel then click **Add** button to add the application.</span></span>

    ![Skills Manager in the results list](./media/skillsmanager-tutorial/tutorial_skillsmanager_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9c508-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9c508-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9c508-136">In this section, you configure and test Azure AD single sign-on with Skills Manager based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9c508-136">In this section, you configure and test Azure AD single sign-on with Skills Manager based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9c508-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Skills Manager is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9c508-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Skills Manager is to a user in Azure AD.</span></span> <span data-ttu-id="9c508-138">In other words, a link relationship between an Azure AD user and the related user in Skills Manager needs to be established.</span><span class="sxs-lookup"><span data-stu-id="9c508-138">In other words, a link relationship between an Azure AD user and the related user in Skills Manager needs to be established.</span></span>

<span data-ttu-id="9c508-139">In Skills Manager, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="9c508-139">In Skills Manager, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9c508-140">To configure and test Azure AD single sign-on with Skills Manager, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="9c508-140">To configure and test Azure AD single sign-on with Skills Manager, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9c508-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="9c508-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="9c508-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9c508-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="9c508-143">**[Create a Skills Manager test user](#create-a-skills-manager-test-user)** - to have a counterpart of Britta Simon in Skills Manager that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="9c508-143">**[Create a Skills Manager test user](#create-a-skills-manager-test-user)** - to have a counterpart of Britta Simon in Skills Manager that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="9c508-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9c508-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="9c508-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="9c508-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9c508-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9c508-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9c508-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skills Manager application.</span><span class="sxs-lookup"><span data-stu-id="9c508-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skills Manager application.</span></span>

<span data-ttu-id="9c508-148">**To configure Azure AD single sign-on with Skills Manager, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9c508-148">**To configure Azure AD single sign-on with Skills Manager, perform the following steps:**</span></span>

1. <span data-ttu-id="9c508-149">In the Azure portal, on the **Skills Manager** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9c508-149">In the Azure portal, on the **Skills Manager** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="9c508-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9c508-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/skillsmanager-tutorial/tutorial_skillsmanager_samlbase.png)

1. <span data-ttu-id="9c508-153">On the **Skills Manager Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9c508-153">On the **Skills Manager Domain and URLs** section, perform the following steps:</span></span>

    ![Skills Manager Domain and URLs single sign-on information](./media/skillsmanager-tutorial/tutorial_skillsmanager_url.png)

    <span data-ttu-id="9c508-155">a.</span><span class="sxs-lookup"><span data-stu-id="9c508-155">a.</span></span> <span data-ttu-id="9c508-156">In the **Identifier** textbox, type a URL using the following pattern: `https://subdomain.skills-manager.com/kennametal`</span><span class="sxs-lookup"><span data-stu-id="9c508-156">In the **Identifier** textbox, type a URL using the following pattern: `https://subdomain.skills-manager.com/kennametal`</span></span>

    <span data-ttu-id="9c508-157">b.</span><span class="sxs-lookup"><span data-stu-id="9c508-157">b.</span></span> <span data-ttu-id="9c508-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://subdomain.skills-manager.com/public/SamlLogin2.aspx`</span><span class="sxs-lookup"><span data-stu-id="9c508-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://subdomain.skills-manager.com/public/SamlLogin2.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9c508-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="9c508-159">These values are not real.</span></span> <span data-ttu-id="9c508-160">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="9c508-160">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="9c508-161">Contact [Skills Manager support team](https://www.ibm.com/support/uk/?lnk=msu_uk) to get these values.</span><span class="sxs-lookup"><span data-stu-id="9c508-161">Contact [Skills Manager support team](https://www.ibm.com/support/uk/?lnk=msu_uk) to get these values.</span></span>
 
1. <span data-ttu-id="9c508-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="9c508-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/skillsmanager-tutorial/tutorial_skillsmanager_certificate.png) 

1. <span data-ttu-id="9c508-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="9c508-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/skillsmanager-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="9c508-166">On the **Skills Manager Configuration** section, click **Configure Skills Manager** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="9c508-166">On the **Skills Manager Configuration** section, click **Configure Skills Manager** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9c508-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="9c508-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Skills Manager Configuration](./media/skillsmanager-tutorial/tutorial_skillsmanager_configure.png) 

1. <span data-ttu-id="9c508-169">To configure single sign-on on **Skills Manager** side, you need to send the downloaded **Certificate(Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Skills Manager support team](https://www.ibm.com/support/uk/?lnk=msu_uk).</span><span class="sxs-lookup"><span data-stu-id="9c508-169">To configure single sign-on on **Skills Manager** side, you need to send the downloaded **Certificate(Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Skills Manager support team](https://www.ibm.com/support/uk/?lnk=msu_uk).</span></span> <span data-ttu-id="9c508-170">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="9c508-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9c508-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="9c508-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9c508-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="9c508-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9c508-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9c508-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9c508-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9c508-174">Create an Azure AD test user</span></span>

<span data-ttu-id="9c508-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9c508-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="9c508-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9c508-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9c508-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="9c508-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/skillsmanager-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="9c508-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="9c508-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/skillsmanager-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="9c508-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="9c508-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/skillsmanager-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="9c508-184">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9c508-184">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/skillsmanager-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9c508-186">a.</span><span class="sxs-lookup"><span data-stu-id="9c508-186">a.</span></span> <span data-ttu-id="9c508-187">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9c508-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9c508-188">b.</span><span class="sxs-lookup"><span data-stu-id="9c508-188">b.</span></span> <span data-ttu-id="9c508-189">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9c508-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="9c508-190">c.</span><span class="sxs-lookup"><span data-stu-id="9c508-190">c.</span></span> <span data-ttu-id="9c508-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="9c508-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="9c508-192">d.</span><span class="sxs-lookup"><span data-stu-id="9c508-192">d.</span></span> <span data-ttu-id="9c508-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="9c508-193">Click **Create**.</span></span>
  
### <a name="create-a-skills-manager-test-user"></a><span data-ttu-id="9c508-194">Create a Skills Manager test user</span><span class="sxs-lookup"><span data-stu-id="9c508-194">Create a Skills Manager test user</span></span>

<span data-ttu-id="9c508-195">In this section, you create a user called Britta Simon in Skills Manager.</span><span class="sxs-lookup"><span data-stu-id="9c508-195">In this section, you create a user called Britta Simon in Skills Manager.</span></span> <span data-ttu-id="9c508-196">Work with [Skills Manager support team](https://www.ibm.com/support/uk/?lnk=msu_uk) to add the users in the Skills Manager platform.</span><span class="sxs-lookup"><span data-stu-id="9c508-196">Work with [Skills Manager support team](https://www.ibm.com/support/uk/?lnk=msu_uk) to add the users in the Skills Manager platform.</span></span> <span data-ttu-id="9c508-197">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9c508-197">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9c508-198">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9c508-198">Assign the Azure AD test user</span></span>

<span data-ttu-id="9c508-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skills Manager.</span><span class="sxs-lookup"><span data-stu-id="9c508-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skills Manager.</span></span>

![Assign the user role][200] 

<span data-ttu-id="9c508-201">**To assign Britta Simon to Skills Manager, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9c508-201">**To assign Britta Simon to Skills Manager, perform the following steps:**</span></span>

1. <span data-ttu-id="9c508-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9c508-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="9c508-204">In the applications list, select **Skills Manager**.</span><span class="sxs-lookup"><span data-stu-id="9c508-204">In the applications list, select **Skills Manager**.</span></span>

    ![The Skills Manager link in the Applications list](./media/skillsmanager-tutorial/tutorial_skillsmanager_app.png)  

1. <span data-ttu-id="9c508-206">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="9c508-206">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="9c508-208">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="9c508-208">Click **Add** button.</span></span> <span data-ttu-id="9c508-209">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9c508-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="9c508-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="9c508-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="9c508-212">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="9c508-212">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="9c508-213">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9c508-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9c508-214">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="9c508-214">Test single sign-on</span></span>

<span data-ttu-id="9c508-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9c508-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9c508-216">When you click the Skills Manager tile in the Access Panel, you should get automatically signed-on to your Skills Manager application.</span><span class="sxs-lookup"><span data-stu-id="9c508-216">When you click the Skills Manager tile in the Access Panel, you should get automatically signed-on to your Skills Manager application.</span></span>
<span data-ttu-id="9c508-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9c508-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9c508-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="9c508-218">Additional resources</span></span>

* [<span data-ttu-id="9c508-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9c508-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="9c508-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9c508-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/skillsmanager-tutorial/tutorial_general_01.png
[2]: ./media/skillsmanager-tutorial/tutorial_general_02.png
[3]: ./media/skillsmanager-tutorial/tutorial_general_03.png
[4]: ./media/skillsmanager-tutorial/tutorial_general_04.png

[100]: ./media/skillsmanager-tutorial/tutorial_general_100.png

[200]: ./media/skillsmanager-tutorial/tutorial_general_200.png
[201]: ./media/skillsmanager-tutorial/tutorial_general_201.png
[202]: ./media/skillsmanager-tutorial/tutorial_general_202.png
[203]: ./media/skillsmanager-tutorial/tutorial_general_203.png

