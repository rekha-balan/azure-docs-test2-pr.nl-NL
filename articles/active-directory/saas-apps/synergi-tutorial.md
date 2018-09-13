---
title: 'Tutorial: Azure Active Directory integration with Synergi | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Synergi.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 73c970e1-f1ba-420b-b225-414fdf93b140
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 91b831be10f71b8f7e5f4226a697ed92eadfd68c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870880"
---
# <a name="tutorial-azure-active-directory-integration-with-synergi"></a><span data-ttu-id="1a769-103">Tutorial: Azure Active Directory integration with Synergi</span><span class="sxs-lookup"><span data-stu-id="1a769-103">Tutorial: Azure Active Directory integration with Synergi</span></span>

<span data-ttu-id="1a769-104">In this tutorial, you learn how to integrate Synergi with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1a769-104">In this tutorial, you learn how to integrate Synergi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1a769-105">Integrating Synergi with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1a769-105">Integrating Synergi with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1a769-106">You can control in Azure AD who has access to Synergi.</span><span class="sxs-lookup"><span data-stu-id="1a769-106">You can control in Azure AD who has access to Synergi.</span></span>
- <span data-ttu-id="1a769-107">You can enable your users to automatically get signed-on to Synergi (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="1a769-107">You can enable your users to automatically get signed-on to Synergi (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="1a769-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1a769-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="1a769-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="1a769-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a769-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1a769-110">Prerequisites</span></span>

<span data-ttu-id="1a769-111">To configure Azure AD integration with Synergi, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1a769-111">To configure Azure AD integration with Synergi, you need the following items:</span></span>

- <span data-ttu-id="1a769-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1a769-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1a769-113">A Synergi single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1a769-113">A Synergi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1a769-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1a769-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1a769-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1a769-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1a769-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="1a769-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1a769-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1a769-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1a769-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="1a769-118">Scenario description</span></span>
<span data-ttu-id="1a769-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1a769-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1a769-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1a769-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1a769-121">Adding Synergi from the gallery</span><span class="sxs-lookup"><span data-stu-id="1a769-121">Adding Synergi from the gallery</span></span>
1. <span data-ttu-id="1a769-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1a769-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-synergi-from-the-gallery"></a><span data-ttu-id="1a769-123">Adding Synergi from the gallery</span><span class="sxs-lookup"><span data-stu-id="1a769-123">Adding Synergi from the gallery</span></span>
<span data-ttu-id="1a769-124">To configure the integration of Synergi into Azure AD, you need to add Synergi from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1a769-124">To configure the integration of Synergi into Azure AD, you need to add Synergi from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1a769-125">**To add Synergi from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1a769-125">**To add Synergi from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1a769-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="1a769-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="1a769-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="1a769-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1a769-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1a769-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="1a769-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="1a769-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="1a769-133">In the search box, type **Synergi**, select **Synergi** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="1a769-133">In the search box, type **Synergi**, select **Synergi** from result panel then click **Add** button to add the application.</span></span>

    ![Synergi in the results list](./media/synergi-tutorial/tutorial_synergi_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1a769-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1a769-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1a769-136">In this section, you configure and test Azure AD single sign-on with Synergi based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1a769-136">In this section, you configure and test Azure AD single sign-on with Synergi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1a769-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Synergi is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a769-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Synergi is to a user in Azure AD.</span></span> <span data-ttu-id="1a769-138">In other words, a link relationship between an Azure AD user and the related user in Synergi needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1a769-138">In other words, a link relationship between an Azure AD user and the related user in Synergi needs to be established.</span></span>

<span data-ttu-id="1a769-139">In Synergi, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="1a769-139">In Synergi, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1a769-140">To configure and test Azure AD single sign-on with Synergi, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1a769-140">To configure and test Azure AD single sign-on with Synergi, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1a769-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1a769-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="1a769-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1a769-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="1a769-143">**[Create a Synergi test user](#create-a-synergi-test-user)** - to have a counterpart of Britta Simon in Synergi that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="1a769-143">**[Create a Synergi test user](#create-a-synergi-test-user)** - to have a counterpart of Britta Simon in Synergi that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="1a769-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1a769-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="1a769-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1a769-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1a769-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1a769-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1a769-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Synergi application.</span><span class="sxs-lookup"><span data-stu-id="1a769-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Synergi application.</span></span>

<span data-ttu-id="1a769-148">**To configure Azure AD single sign-on with Synergi, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1a769-148">**To configure Azure AD single sign-on with Synergi, perform the following steps:**</span></span>

1. <span data-ttu-id="1a769-149">In the Azure portal, on the **Synergi** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1a769-149">In the Azure portal, on the **Synergi** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="1a769-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1a769-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/synergi-tutorial/tutorial_synergi_samlbase.png)

1. <span data-ttu-id="1a769-153">On the **Synergi Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1a769-153">On the **Synergi Domain and URLs** section, perform the following steps:</span></span>

    ![Synergi Domain and URLs single sign-on information](./media/synergi-tutorial/tutorial_synergi_url.png)

    <span data-ttu-id="1a769-155">a.</span><span class="sxs-lookup"><span data-stu-id="1a769-155">a.</span></span> <span data-ttu-id="1a769-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.irmsecurity.com`</span><span class="sxs-lookup"><span data-stu-id="1a769-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.irmsecurity.com`</span></span>

    <span data-ttu-id="1a769-157">b.</span><span class="sxs-lookup"><span data-stu-id="1a769-157">b.</span></span> <span data-ttu-id="1a769-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.irmsecurity.com/sso/<organization id>`</span><span class="sxs-lookup"><span data-stu-id="1a769-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.irmsecurity.com/sso/<organization id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1a769-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="1a769-159">These values are not real.</span></span> <span data-ttu-id="1a769-160">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="1a769-160">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="1a769-161">Contact [Synergi support team](https://www.irmsecurity.com/contact/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="1a769-161">Contact [Synergi support team](https://www.irmsecurity.com/contact/) to get these values.</span></span>

1. <span data-ttu-id="1a769-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="1a769-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/synergi-tutorial/tutorial_synergi_certificate.png) 

1. <span data-ttu-id="1a769-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="1a769-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/synergi-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="1a769-166">On the **Synergi Configuration** section, click **Configure Synergi** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="1a769-166">On the **Synergi Configuration** section, click **Configure Synergi** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1a769-167">Copy the **Sign-Out URL and SAML Entity ID** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="1a769-167">Copy the **Sign-Out URL and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Synergi Configuration](./media/synergi-tutorial/tutorial_synergi_configure.png) 

1. <span data-ttu-id="1a769-169">To configure single sign-on on **Synergi** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, and SAML Entity ID** to [Synergi support team](https://www.irmsecurity.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="1a769-169">To configure single sign-on on **Synergi** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, and SAML Entity ID** to [Synergi support team](https://www.irmsecurity.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="1a769-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="1a769-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1a769-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="1a769-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1a769-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1a769-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1a769-173">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1a769-173">Create an Azure AD test user</span></span>

<span data-ttu-id="1a769-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1a769-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="1a769-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1a769-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1a769-177">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="1a769-177">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/synergi-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="1a769-179">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="1a769-179">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/synergi-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="1a769-181">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="1a769-181">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/synergi-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="1a769-183">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1a769-183">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/synergi-tutorial/create_aaduser_04.png)

    <span data-ttu-id="1a769-185">a.</span><span class="sxs-lookup"><span data-stu-id="1a769-185">a.</span></span> <span data-ttu-id="1a769-186">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1a769-186">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1a769-187">b.</span><span class="sxs-lookup"><span data-stu-id="1a769-187">b.</span></span> <span data-ttu-id="1a769-188">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1a769-188">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="1a769-189">c.</span><span class="sxs-lookup"><span data-stu-id="1a769-189">c.</span></span> <span data-ttu-id="1a769-190">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="1a769-190">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="1a769-191">d.</span><span class="sxs-lookup"><span data-stu-id="1a769-191">d.</span></span> <span data-ttu-id="1a769-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1a769-192">Click **Create**.</span></span>
  
### <a name="create-a-synergi-test-user"></a><span data-ttu-id="1a769-193">Create a Synergi test user</span><span class="sxs-lookup"><span data-stu-id="1a769-193">Create a Synergi test user</span></span>

<span data-ttu-id="1a769-194">In this section, you create a user called Britta Simon in Synergi.</span><span class="sxs-lookup"><span data-stu-id="1a769-194">In this section, you create a user called Britta Simon in Synergi.</span></span> <span data-ttu-id="1a769-195">Work with [Synergi support team](https://www.irmsecurity.com/contact/) to add the users in the Synergi platform.</span><span class="sxs-lookup"><span data-stu-id="1a769-195">Work with [Synergi support team](https://www.irmsecurity.com/contact/) to add the users in the Synergi platform.</span></span> <span data-ttu-id="1a769-196">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1a769-196">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1a769-197">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1a769-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="1a769-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Synergi.</span><span class="sxs-lookup"><span data-stu-id="1a769-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Synergi.</span></span>

![Assign the user role][200] 

<span data-ttu-id="1a769-200">**To assign Britta Simon to Synergi, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1a769-200">**To assign Britta Simon to Synergi, perform the following steps:**</span></span>

1. <span data-ttu-id="1a769-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1a769-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="1a769-203">In the applications list, select **Synergi**.</span><span class="sxs-lookup"><span data-stu-id="1a769-203">In the applications list, select **Synergi**.</span></span>

    ![The Synergi link in the Applications list](./media/synergi-tutorial/tutorial_synergi_app.png)  

1. <span data-ttu-id="1a769-205">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="1a769-205">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="1a769-207">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="1a769-207">Click **Add** button.</span></span> <span data-ttu-id="1a769-208">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1a769-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="1a769-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="1a769-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="1a769-211">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="1a769-211">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="1a769-212">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1a769-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1a769-213">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="1a769-213">Test single sign-on</span></span>

<span data-ttu-id="1a769-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1a769-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1a769-215">When you click the Synergi tile in the Access Panel, you should get automatically signed-on to your Synergi application.</span><span class="sxs-lookup"><span data-stu-id="1a769-215">When you click the Synergi tile in the Access Panel, you should get automatically signed-on to your Synergi application.</span></span>
<span data-ttu-id="1a769-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1a769-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1a769-217">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1a769-217">Additional resources</span></span>

* [<span data-ttu-id="1a769-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a769-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="1a769-219">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1a769-219">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/synergi-tutorial/tutorial_general_01.png
[2]: ./media/synergi-tutorial/tutorial_general_02.png
[3]: ./media/synergi-tutorial/tutorial_general_03.png
[4]: ./media/synergi-tutorial/tutorial_general_04.png

[100]: ./media/synergi-tutorial/tutorial_general_100.png

[200]: ./media/synergi-tutorial/tutorial_general_200.png
[201]: ./media/synergi-tutorial/tutorial_general_201.png
[202]: ./media/synergi-tutorial/tutorial_general_202.png
[203]: ./media/synergi-tutorial/tutorial_general_203.png

