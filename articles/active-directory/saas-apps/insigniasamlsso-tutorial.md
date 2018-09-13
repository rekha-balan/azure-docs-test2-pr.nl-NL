---
title: 'Tutorial: Azure Active Directory integration with Insignia SAML SSO | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Insignia SAML SSO.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 828c981c-c3dd-4eb2-8699-0f732baa43f6
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: jeedes
ms.openlocfilehash: 776ad8445c1968928a631ae1a401db4c65a6bb6d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868344"
---
# <a name="tutorial-azure-active-directory-integration-with-insignia-saml-sso"></a><span data-ttu-id="6fe02-103">Tutorial: Azure Active Directory integration with Insignia SAML SSO</span><span class="sxs-lookup"><span data-stu-id="6fe02-103">Tutorial: Azure Active Directory integration with Insignia SAML SSO</span></span>

<span data-ttu-id="6fe02-104">In this tutorial, you learn how to integrate Insignia SAML SSO with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6fe02-104">In this tutorial, you learn how to integrate Insignia SAML SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6fe02-105">Integrating Insignia SAML SSO with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="6fe02-105">Integrating Insignia SAML SSO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6fe02-106">You can control in Azure AD who has access to Insignia SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="6fe02-106">You can control in Azure AD who has access to Insignia SAML SSO.</span></span>
- <span data-ttu-id="6fe02-107">You can enable your users to automatically get signed-on to Insignia SAML SSO (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="6fe02-107">You can enable your users to automatically get signed-on to Insignia SAML SSO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6fe02-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6fe02-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="6fe02-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="6fe02-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fe02-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6fe02-110">Prerequisites</span></span>

<span data-ttu-id="6fe02-111">To configure Azure AD integration with Insignia SAML SSO, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="6fe02-111">To configure Azure AD integration with Insignia SAML SSO, you need the following items:</span></span>

- <span data-ttu-id="6fe02-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="6fe02-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6fe02-113">An Insignia SAML SSO single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="6fe02-113">An Insignia SAML SSO single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6fe02-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="6fe02-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6fe02-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="6fe02-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6fe02-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="6fe02-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6fe02-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6fe02-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6fe02-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="6fe02-118">Scenario description</span></span>
<span data-ttu-id="6fe02-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="6fe02-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6fe02-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="6fe02-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6fe02-121">Adding Insignia SAML SSO from the gallery</span><span class="sxs-lookup"><span data-stu-id="6fe02-121">Adding Insignia SAML SSO from the gallery</span></span>
1. <span data-ttu-id="6fe02-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6fe02-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insignia-saml-sso-from-the-gallery"></a><span data-ttu-id="6fe02-123">Adding Insignia SAML SSO from the gallery</span><span class="sxs-lookup"><span data-stu-id="6fe02-123">Adding Insignia SAML SSO from the gallery</span></span>
<span data-ttu-id="6fe02-124">To configure the integration of Insignia SAML SSO into Azure AD, you need to add Insignia SAML SSO from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="6fe02-124">To configure the integration of Insignia SAML SSO into Azure AD, you need to add Insignia SAML SSO from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6fe02-125">**To add Insignia SAML SSO from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6fe02-125">**To add Insignia SAML SSO from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6fe02-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="6fe02-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="6fe02-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="6fe02-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6fe02-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6fe02-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="6fe02-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="6fe02-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="6fe02-133">In the search box, type **Insignia SAML SSO**, select **Insignia SAML SSO** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="6fe02-133">In the search box, type **Insignia SAML SSO**, select **Insignia SAML SSO** from result panel then click **Add** button to add the application.</span></span>

    ![Insignia SAML SSO in the results list](./media/insigniasamlsso-tutorial/tutorial_insigniasamlsso_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6fe02-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6fe02-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6fe02-136">In this section, you configure and test Azure AD single sign-on with Insignia SAML SSO based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6fe02-136">In this section, you configure and test Azure AD single sign-on with Insignia SAML SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6fe02-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Insignia SAML SSO is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6fe02-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Insignia SAML SSO is to a user in Azure AD.</span></span> <span data-ttu-id="6fe02-138">In other words, a link relationship between an Azure AD user and the related user in Insignia SAML SSO needs to be established.</span><span class="sxs-lookup"><span data-stu-id="6fe02-138">In other words, a link relationship between an Azure AD user and the related user in Insignia SAML SSO needs to be established.</span></span>

<span data-ttu-id="6fe02-139">In Insignia SAML SSO, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="6fe02-139">In Insignia SAML SSO, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6fe02-140">To configure and test Azure AD single sign-on with Insignia SAML SSO, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6fe02-140">To configure and test Azure AD single sign-on with Insignia SAML SSO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6fe02-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="6fe02-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="6fe02-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6fe02-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="6fe02-143">**[Create an Insignia SAML SSO test user](#create-an-insignia-saml-sso-test-user)** - to have a counterpart of Britta Simon in Insignia SAML SSO that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="6fe02-143">**[Create an Insignia SAML SSO test user](#create-an-insignia-saml-sso-test-user)** - to have a counterpart of Britta Simon in Insignia SAML SSO that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="6fe02-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6fe02-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="6fe02-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="6fe02-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6fe02-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6fe02-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6fe02-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Insignia SAML SSO application.</span><span class="sxs-lookup"><span data-stu-id="6fe02-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Insignia SAML SSO application.</span></span>

<span data-ttu-id="6fe02-148">**To configure Azure AD single sign-on with Insignia SAML SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6fe02-148">**To configure Azure AD single sign-on with Insignia SAML SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="6fe02-149">In the Azure portal, on the **Insignia SAML SSO** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6fe02-149">In the Azure portal, on the **Insignia SAML SSO** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="6fe02-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6fe02-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/insigniasamlsso-tutorial/tutorial_insigniasamlsso_samlbase.png)

1. <span data-ttu-id="6fe02-153">On the **Insignia SAML SSO Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6fe02-153">On the **Insignia SAML SSO Domain and URLs** section, perform the following steps:</span></span>

    ![Insignia SAML SSO Domain and URLs single sign-on information](./media/insigniasamlsso-tutorial/tutorial_insigniasamlsso_url.png)

    <span data-ttu-id="6fe02-155">a.</span><span class="sxs-lookup"><span data-stu-id="6fe02-155">a.</span></span> <span data-ttu-id="6fe02-156">In the **Sign-on URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="6fe02-156">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<customername>.insigniails.com/ils` |
    | `https://<customername>.insigniails.com/` |
    | `https://<customername>.insigniailsusa.com/ ` |

    <span data-ttu-id="6fe02-157">b.</span><span class="sxs-lookup"><span data-stu-id="6fe02-157">b.</span></span> <span data-ttu-id="6fe02-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<customername>.insigniailsusa.com/<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="6fe02-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<customername>.insigniailsusa.com/<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6fe02-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="6fe02-159">These values are not real.</span></span> <span data-ttu-id="6fe02-160">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="6fe02-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6fe02-161">Contact [Insignia SAML SSO Client support team](http://www.insigniasoftware.com/insignia/Techsupport.aspx) to get these values.</span><span class="sxs-lookup"><span data-stu-id="6fe02-161">Contact [Insignia SAML SSO Client support team](http://www.insigniasoftware.com/insignia/Techsupport.aspx) to get these values.</span></span> 
 

1. <span data-ttu-id="6fe02-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="6fe02-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/insigniasamlsso-tutorial/tutorial_insigniasamlsso_certificate.png) 

1. <span data-ttu-id="6fe02-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="6fe02-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/insigniasamlsso-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="6fe02-166">On the **Insignia SAML SSO Configuration** section, click **Configure Insignia SAML SSO** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="6fe02-166">On the **Insignia SAML SSO Configuration** section, click **Configure Insignia SAML SSO** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6fe02-167">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="6fe02-167">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Insignia SAML SSO Configuration](./media/insigniasamlsso-tutorial/tutorial_insigniasamlsso_configure.png) 

1. <span data-ttu-id="6fe02-169">To configure single sign-on on **Insignia SAML SSO** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, and SAML Single Sign-On Service URL** to [Insignia SAML SSO support team](http://www.insigniasoftware.com/insignia/Techsupport.aspx).</span><span class="sxs-lookup"><span data-stu-id="6fe02-169">To configure single sign-on on **Insignia SAML SSO** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, and SAML Single Sign-On Service URL** to [Insignia SAML SSO support team](http://www.insigniasoftware.com/insignia/Techsupport.aspx).</span></span> <span data-ttu-id="6fe02-170">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="6fe02-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="6fe02-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="6fe02-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6fe02-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="6fe02-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6fe02-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6fe02-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6fe02-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6fe02-174">Create an Azure AD test user</span></span>

<span data-ttu-id="6fe02-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6fe02-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="6fe02-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6fe02-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6fe02-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="6fe02-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/insigniasamlsso-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="6fe02-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="6fe02-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/insigniasamlsso-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="6fe02-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="6fe02-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/insigniasamlsso-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="6fe02-184">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6fe02-184">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/insigniasamlsso-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6fe02-186">a.</span><span class="sxs-lookup"><span data-stu-id="6fe02-186">a.</span></span> <span data-ttu-id="6fe02-187">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6fe02-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6fe02-188">b.</span><span class="sxs-lookup"><span data-stu-id="6fe02-188">b.</span></span> <span data-ttu-id="6fe02-189">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6fe02-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="6fe02-190">c.</span><span class="sxs-lookup"><span data-stu-id="6fe02-190">c.</span></span> <span data-ttu-id="6fe02-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="6fe02-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="6fe02-192">d.</span><span class="sxs-lookup"><span data-stu-id="6fe02-192">d.</span></span> <span data-ttu-id="6fe02-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6fe02-193">Click **Create**.</span></span>
 
### <a name="create-an-insignia-saml-sso-test-user"></a><span data-ttu-id="6fe02-194">Create an Insignia SAML SSO test user</span><span class="sxs-lookup"><span data-stu-id="6fe02-194">Create an Insignia SAML SSO test user</span></span>

<span data-ttu-id="6fe02-195">In this section, you create a user called Britta Simon in Insignia Library System.</span><span class="sxs-lookup"><span data-stu-id="6fe02-195">In this section, you create a user called Britta Simon in Insignia Library System.</span></span> <span data-ttu-id="6fe02-196">Work with [Insignia Library System support team](http://www.insigniasoftware.com/insignia/Techsupport.aspx) to add the users in the Insignia Library System platform.</span><span class="sxs-lookup"><span data-stu-id="6fe02-196">Work with [Insignia Library System support team](http://www.insigniasoftware.com/insignia/Techsupport.aspx) to add the users in the Insignia Library System platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6fe02-197">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6fe02-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="6fe02-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Insignia SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="6fe02-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Insignia SAML SSO.</span></span>

![Assign the user role][200] 

<span data-ttu-id="6fe02-200">**To assign Britta Simon to Insignia SAML SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6fe02-200">**To assign Britta Simon to Insignia SAML SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="6fe02-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6fe02-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="6fe02-203">In the applications list, select **Insignia SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="6fe02-203">In the applications list, select **Insignia SAML SSO**.</span></span>

    ![The Insignia SAML SSO link in the Applications list](./media/insigniasamlsso-tutorial/tutorial_insigniasamlsso_app.png)  

1. <span data-ttu-id="6fe02-205">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="6fe02-205">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="6fe02-207">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="6fe02-207">Click **Add** button.</span></span> <span data-ttu-id="6fe02-208">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6fe02-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="6fe02-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="6fe02-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="6fe02-211">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="6fe02-211">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="6fe02-212">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6fe02-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6fe02-213">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="6fe02-213">Test single sign-on</span></span>

<span data-ttu-id="6fe02-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="6fe02-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6fe02-215">When you click the Insignia SAML SSO tile in the Access Panel, you should get automatically signed-on to your Insignia SAML SSO application.</span><span class="sxs-lookup"><span data-stu-id="6fe02-215">When you click the Insignia SAML SSO tile in the Access Panel, you should get automatically signed-on to your Insignia SAML SSO application.</span></span>
<span data-ttu-id="6fe02-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6fe02-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6fe02-217">Additional resources</span><span class="sxs-lookup"><span data-stu-id="6fe02-217">Additional resources</span></span>

* [<span data-ttu-id="6fe02-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6fe02-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="6fe02-219">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6fe02-219">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/insigniasamlsso-tutorial/tutorial_general_01.png
[2]: ./media/insigniasamlsso-tutorial/tutorial_general_02.png
[3]: ./media/insigniasamlsso-tutorial/tutorial_general_03.png
[4]: ./media/insigniasamlsso-tutorial/tutorial_general_04.png

[100]: ./media/insigniasamlsso-tutorial/tutorial_general_100.png

[200]: ./media/insigniasamlsso-tutorial/tutorial_general_200.png
[201]: ./media/insigniasamlsso-tutorial/tutorial_general_201.png
[202]: ./media/insigniasamlsso-tutorial/tutorial_general_202.png
[203]: ./media/insigniasamlsso-tutorial/tutorial_general_203.png

