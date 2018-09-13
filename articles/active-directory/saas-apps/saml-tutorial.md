---
title: 'Tutorial: Azure Active Directory integration with SAML 1.1 Token enabled LOB App | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SAML 1.1 Token enabled LOB App.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ced1d88d-0e48-40d5-9aea-ef991cd9d270
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2018
ms.author: jeedes
ms.openlocfilehash: edabc09f820093d088ec0b8ed1222fb26c800bee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867802"
---
# <a name="tutorial-azure-active-directory-integration-with-saml-11-token-enabled-lob-app"></a><span data-ttu-id="cbfa9-103">Tutorial: Azure Active Directory integration with SAML 1.1 Token enabled LOB App</span><span class="sxs-lookup"><span data-stu-id="cbfa9-103">Tutorial: Azure Active Directory integration with SAML 1.1 Token enabled LOB App</span></span>

<span data-ttu-id="cbfa9-104">In this tutorial, you learn how to integrate SAML 1.1 Token enabled LOB App with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cbfa9-104">In this tutorial, you learn how to integrate SAML 1.1 Token enabled LOB App with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cbfa9-105">Integrating SAML 1.1 Token enabled LOB App with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="cbfa9-105">Integrating SAML 1.1 Token enabled LOB App with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cbfa9-106">You can control in Azure AD who has access to SAML 1.1 Token enabled LOB App.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-106">You can control in Azure AD who has access to SAML 1.1 Token enabled LOB App.</span></span>
- <span data-ttu-id="cbfa9-107">You can enable your users to automatically get signed-on to SAML 1.1 Token enabled LOB App (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-107">You can enable your users to automatically get signed-on to SAML 1.1 Token enabled LOB App (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="cbfa9-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="cbfa9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="cbfa9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbfa9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cbfa9-110">Prerequisites</span></span>

<span data-ttu-id="cbfa9-111">To configure Azure AD integration with SAML 1.1 Token enabled LOB App, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="cbfa9-111">To configure Azure AD integration with SAML 1.1 Token enabled LOB App, you need the following items:</span></span>

- <span data-ttu-id="cbfa9-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="cbfa9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cbfa9-113">A SAML 1.1 Token enabled LOB App single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="cbfa9-113">A SAML 1.1 Token enabled LOB App single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cbfa9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cbfa9-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="cbfa9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cbfa9-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cbfa9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cbfa9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cbfa9-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="cbfa9-118">Scenario description</span></span>
<span data-ttu-id="cbfa9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cbfa9-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="cbfa9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cbfa9-121">Adding SAML 1.1 Token enabled LOB App from the gallery</span><span class="sxs-lookup"><span data-stu-id="cbfa9-121">Adding SAML 1.1 Token enabled LOB App from the gallery</span></span>
1. <span data-ttu-id="cbfa9-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cbfa9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-11-token-enabled-lob-app-from-the-gallery"></a><span data-ttu-id="cbfa9-123">Adding SAML 1.1 Token enabled LOB App from the gallery</span><span class="sxs-lookup"><span data-stu-id="cbfa9-123">Adding SAML 1.1 Token enabled LOB App from the gallery</span></span>
<span data-ttu-id="cbfa9-124">To configure the integration of SAML 1.1 Token enabled LOB App into Azure AD, you need to add SAML 1.1 Token enabled LOB App from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-124">To configure the integration of SAML 1.1 Token enabled LOB App into Azure AD, you need to add SAML 1.1 Token enabled LOB App from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cbfa9-125">**To add SAML 1.1 Token enabled LOB App from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cbfa9-125">**To add SAML 1.1 Token enabled LOB App from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cbfa9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="cbfa9-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cbfa9-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="cbfa9-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="cbfa9-133">In the search box, type **SAML 1.1 Token enabled LOB App**, select **SAML 1.1 Token enabled LOB App** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-133">In the search box, type **SAML 1.1 Token enabled LOB App**, select **SAML 1.1 Token enabled LOB App** from result panel then click **Add** button to add the application.</span></span>

    ![SAML 1.1 Token enabled LOB App in the results list](./media/saml-tutorial/tutorial_saml_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="cbfa9-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cbfa9-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="cbfa9-136">In this section, you configure and test Azure AD single sign-on with SAML 1.1 Token enabled LOB App based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cbfa9-136">In this section, you configure and test Azure AD single sign-on with SAML 1.1 Token enabled LOB App based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cbfa9-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SAML 1.1 Token enabled LOB App is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SAML 1.1 Token enabled LOB App is to a user in Azure AD.</span></span> <span data-ttu-id="cbfa9-138">In other words, a link relationship between an Azure AD user and the related user in SAML 1.1 Token enabled LOB App needs to be established.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-138">In other words, a link relationship between an Azure AD user and the related user in SAML 1.1 Token enabled LOB App needs to be established.</span></span>

<span data-ttu-id="cbfa9-139">To configure and test Azure AD single sign-on with SAML 1.1 Token enabled LOB App, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="cbfa9-139">To configure and test Azure AD single sign-on with SAML 1.1 Token enabled LOB App, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cbfa9-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="cbfa9-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="cbfa9-142">**[Create a SAML 1.1 Token enabled LOB App test user](#create-a-saml-11-token-enabled-lob-app-test-user)** - to have a counterpart of Britta Simon in SAML 1.1 Token enabled LOB App that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-142">**[Create a SAML 1.1 Token enabled LOB App test user](#create-a-saml-11-token-enabled-lob-app-test-user)** - to have a counterpart of Britta Simon in SAML 1.1 Token enabled LOB App that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="cbfa9-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="cbfa9-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="cbfa9-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cbfa9-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="cbfa9-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML 1.1 Token enabled LOB App application.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML 1.1 Token enabled LOB App application.</span></span>

<span data-ttu-id="cbfa9-147">**To configure Azure AD single sign-on with SAML 1.1 Token enabled LOB App, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cbfa9-147">**To configure Azure AD single sign-on with SAML 1.1 Token enabled LOB App, perform the following steps:**</span></span>

1. <span data-ttu-id="cbfa9-148">In the Azure portal, on the **SAML 1.1 Token enabled LOB App** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-148">In the Azure portal, on the **SAML 1.1 Token enabled LOB App** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="cbfa9-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/saml-tutorial/tutorial_saml_samlbase.png)

1. <span data-ttu-id="cbfa9-152">On the **SAML 1.1 Token enabled LOB App Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cbfa9-152">On the **SAML 1.1 Token enabled LOB App Domain and URLs** section, perform the following steps:</span></span>

    ![SAML 1.1 Token enabled LOB App Domain and URLs single sign-on information](./media/saml-tutorial/tutorial_saml_url.png)

    <span data-ttu-id="cbfa9-154">a.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-154">a.</span></span> <span data-ttu-id="cbfa9-155">In the **Sign on URL** textbox, type a URL using the following pattern: `https://your-app-url`</span><span class="sxs-lookup"><span data-stu-id="cbfa9-155">In the **Sign on URL** textbox, type a URL using the following pattern: `https://your-app-url`</span></span>

    <span data-ttu-id="cbfa9-156">b.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-156">b.</span></span> <span data-ttu-id="cbfa9-157">In the **Identifier (Entity ID)** textbox, type a URL using the following pattern: `https://your-app-url`</span><span class="sxs-lookup"><span data-stu-id="cbfa9-157">In the **Identifier (Entity ID)** textbox, type a URL using the following pattern: `https://your-app-url`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="cbfa9-158">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-158">These values are not real.</span></span> <span data-ttu-id="cbfa9-159">Please replace these values with application specific urls.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-159">Please replace these values with application specific urls.</span></span>  

1. <span data-ttu-id="cbfa9-160">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-160">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/saml-tutorial/tutorial_saml_certificate.png) 

1. <span data-ttu-id="cbfa9-162">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-162">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/saml-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="cbfa9-164">On the **SAML 1.1 Token enabled LOB App Configuration** section, click **Configure SAML 1.1 Token enabled LOB App** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-164">On the **SAML 1.1 Token enabled LOB App Configuration** section, click **Configure SAML 1.1 Token enabled LOB App** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cbfa9-165">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="cbfa9-165">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![SAML 1.1 Token enabled LOB App Configuration](./media/saml-tutorial/tutorial_saml_configure.png) 

1. <span data-ttu-id="cbfa9-167">To configure single sign-on on **SAML 1.1 Token enabled LOB App** side, you need to send the downloaded **Certificate (Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to application support team.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-167">To configure single sign-on on **SAML 1.1 Token enabled LOB App** side, you need to send the downloaded **Certificate (Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to application support team.</span></span> <span data-ttu-id="cbfa9-168">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-168">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="cbfa9-169">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cbfa9-169">Create an Azure AD test user</span></span>

<span data-ttu-id="cbfa9-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="cbfa9-172">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cbfa9-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cbfa9-173">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-173">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/saml-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="cbfa9-175">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-175">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/saml-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="cbfa9-177">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-177">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/saml-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="cbfa9-179">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cbfa9-179">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/saml-tutorial/create_aaduser_04.png)

    <span data-ttu-id="cbfa9-181">a.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-181">a.</span></span> <span data-ttu-id="cbfa9-182">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-182">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cbfa9-183">b.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-183">b.</span></span> <span data-ttu-id="cbfa9-184">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-184">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="cbfa9-185">c.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-185">c.</span></span> <span data-ttu-id="cbfa9-186">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-186">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="cbfa9-187">d.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-187">d.</span></span> <span data-ttu-id="cbfa9-188">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-188">Click **Create**.</span></span>
 
### <a name="create-a-saml-11-token-enabled-lob-app-test-user"></a><span data-ttu-id="cbfa9-189">Create a SAML 1.1 Token enabled LOB App test user</span><span class="sxs-lookup"><span data-stu-id="cbfa9-189">Create a SAML 1.1 Token enabled LOB App test user</span></span>

<span data-ttu-id="cbfa9-190">In this section, you create a user called Britta Simon in SAML 1.1 Token enabled LOB App.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-190">In this section, you create a user called Britta Simon in SAML 1.1 Token enabled LOB App.</span></span> <span data-ttu-id="cbfa9-191">Work with application support team to create user on application side.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-191">Work with application support team to create user on application side.</span></span> <span data-ttu-id="cbfa9-192">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-192">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="cbfa9-193">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cbfa9-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="cbfa9-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML 1.1 Token enabled LOB App.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML 1.1 Token enabled LOB App.</span></span>

![Assign the user role][200] 

<span data-ttu-id="cbfa9-196">**To assign Britta Simon to SAML 1.1 Token enabled LOB App, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cbfa9-196">**To assign Britta Simon to SAML 1.1 Token enabled LOB App, perform the following steps:**</span></span>

1. <span data-ttu-id="cbfa9-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="cbfa9-199">In the applications list, select **SAML 1.1 Token enabled LOB App**.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-199">In the applications list, select **SAML 1.1 Token enabled LOB App**.</span></span>

    ![The SAML 1.1 Token enabled LOB App link in the Applications list](./media/saml-tutorial/tutorial_saml_app.png)  

1. <span data-ttu-id="cbfa9-201">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-201">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="cbfa9-203">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-203">Click **Add** button.</span></span> <span data-ttu-id="cbfa9-204">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="cbfa9-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="cbfa9-207">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-207">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="cbfa9-208">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="cbfa9-209">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="cbfa9-209">Test single sign-on</span></span>

<span data-ttu-id="cbfa9-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cbfa9-211">When you click the SAML 1.1 Token enabled LOB App tile in the Access Panel, you should get automatically signed-on to your SAML 1.1 Token enabled LOB App application.</span><span class="sxs-lookup"><span data-stu-id="cbfa9-211">When you click the SAML 1.1 Token enabled LOB App tile in the Access Panel, you should get automatically signed-on to your SAML 1.1 Token enabled LOB App application.</span></span>
<span data-ttu-id="cbfa9-212">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cbfa9-212">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cbfa9-213">Additional resources</span><span class="sxs-lookup"><span data-stu-id="cbfa9-213">Additional resources</span></span>

* [<span data-ttu-id="cbfa9-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cbfa9-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="cbfa9-215">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cbfa9-215">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/saml-tutorial/tutorial_general_01.png
[2]: ./media/saml-tutorial/tutorial_general_02.png
[3]: ./media/saml-tutorial/tutorial_general_03.png
[4]: ./media/saml-tutorial/tutorial_general_04.png

[100]: ./media/saml-tutorial/tutorial_general_100.png

[200]: ./media/saml-tutorial/tutorial_general_200.png
[201]: ./media/saml-tutorial/tutorial_general_201.png
[202]: ./media/saml-tutorial/tutorial_general_202.png
[203]: ./media/saml-tutorial/tutorial_general_203.png
