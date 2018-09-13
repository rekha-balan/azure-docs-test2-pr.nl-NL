---
title: 'Tutorial: Azure Active Directory integration with Peoplecart | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Peoplecart.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: c83b5d9d-2638-4689-b9f0-f56a9159e7a0
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: bfd2032df8cdb2b7b65a0740ba075d4ea00cbd51
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856915"
---
# <a name="tutorial-azure-active-directory-integration-with-peoplecart"></a><span data-ttu-id="8d03f-103">Tutorial: Azure Active Directory integration with Peoplecart</span><span class="sxs-lookup"><span data-stu-id="8d03f-103">Tutorial: Azure Active Directory integration with Peoplecart</span></span>

<span data-ttu-id="8d03f-104">In this tutorial, you learn how to integrate Peoplecart with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8d03f-104">In this tutorial, you learn how to integrate Peoplecart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d03f-105">Integrating Peoplecart with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8d03f-105">Integrating Peoplecart with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8d03f-106">You can control in Azure AD who has access to Peoplecart</span><span class="sxs-lookup"><span data-stu-id="8d03f-106">You can control in Azure AD who has access to Peoplecart</span></span>
- <span data-ttu-id="8d03f-107">You can enable your users to automatically get signed-on to Peoplecart (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="8d03f-107">You can enable your users to automatically get signed-on to Peoplecart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8d03f-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8d03f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8d03f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="8d03f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d03f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8d03f-110">Prerequisites</span></span>

<span data-ttu-id="8d03f-111">To configure Azure AD integration with Peoplecart, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8d03f-111">To configure Azure AD integration with Peoplecart, you need the following items:</span></span>

- <span data-ttu-id="8d03f-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8d03f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d03f-113">A Peoplecart single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8d03f-113">A Peoplecart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d03f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8d03f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8d03f-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8d03f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8d03f-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="8d03f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d03f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d03f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d03f-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8d03f-118">Scenario description</span></span>
<span data-ttu-id="8d03f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8d03f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8d03f-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8d03f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d03f-121">Adding Peoplecart from the gallery</span><span class="sxs-lookup"><span data-stu-id="8d03f-121">Adding Peoplecart from the gallery</span></span>
1. <span data-ttu-id="8d03f-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8d03f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-peoplecart-from-the-gallery"></a><span data-ttu-id="8d03f-123">Adding Peoplecart from the gallery</span><span class="sxs-lookup"><span data-stu-id="8d03f-123">Adding Peoplecart from the gallery</span></span>
<span data-ttu-id="8d03f-124">To configure the integration of Peoplecart into Azure AD, you need to add Peoplecart from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8d03f-124">To configure the integration of Peoplecart into Azure AD, you need to add Peoplecart from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8d03f-125">**To add Peoplecart from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8d03f-125">**To add Peoplecart from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8d03f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8d03f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="8d03f-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="8d03f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8d03f-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8d03f-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="8d03f-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="8d03f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="8d03f-133">In the search box, type **Peoplecart**, select **Peoplecart** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="8d03f-133">In the search box, type **Peoplecart**, select **Peoplecart** from result panel then click **Add** button to add the application.</span></span>

    ![Peoplecart in the results list](./media/peoplecart-tutorial/tutorial_peoplecart_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8d03f-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8d03f-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="8d03f-136">In this section, you configure and test Azure AD single sign-on with Peoplecart based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8d03f-136">In this section, you configure and test Azure AD single sign-on with Peoplecart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8d03f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Peoplecart is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d03f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Peoplecart is to a user in Azure AD.</span></span> <span data-ttu-id="8d03f-138">In other words, a link relationship between an Azure AD user and the related user in Peoplecart needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8d03f-138">In other words, a link relationship between an Azure AD user and the related user in Peoplecart needs to be established.</span></span>

<span data-ttu-id="8d03f-139">In Peoplecart, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="8d03f-139">In Peoplecart, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8d03f-140">To configure and test Azure AD single sign-on with Peoplecart, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8d03f-140">To configure and test Azure AD single sign-on with Peoplecart, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8d03f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8d03f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="8d03f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d03f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="8d03f-143">**[Create a Peoplecart test user](#create-a-peoplecart-test-user)** - to have a counterpart of Britta Simon in Peoplecart that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="8d03f-143">**[Create a Peoplecart test user](#create-a-peoplecart-test-user)** - to have a counterpart of Britta Simon in Peoplecart that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="8d03f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8d03f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="8d03f-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8d03f-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8d03f-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8d03f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8d03f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Peoplecart application.</span><span class="sxs-lookup"><span data-stu-id="8d03f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Peoplecart application.</span></span>

<span data-ttu-id="8d03f-148">**To configure Azure AD single sign-on with Peoplecart, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8d03f-148">**To configure Azure AD single sign-on with Peoplecart, perform the following steps:**</span></span>

1. <span data-ttu-id="8d03f-149">In the Azure portal, on the **Peoplecart** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8d03f-149">In the Azure portal, on the **Peoplecart** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="8d03f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8d03f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/peoplecart-tutorial/tutorial_peoplecart_samlbase.png)

1. <span data-ttu-id="8d03f-153">On the **Peoplecart Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8d03f-153">On the **Peoplecart Domain and URLs** section, perform the following steps:</span></span>

    ![Peoplecart Domain and URLs single sign-on information](./media/peoplecart-tutorial/tutorial_peoplecart_url.png)

    <span data-ttu-id="8d03f-155">a.</span><span class="sxs-lookup"><span data-stu-id="8d03f-155">a.</span></span> <span data-ttu-id="8d03f-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.peoplecart.com/SignIn.aspx`</span><span class="sxs-lookup"><span data-stu-id="8d03f-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.peoplecart.com/SignIn.aspx`</span></span>

    <span data-ttu-id="8d03f-157">b.</span><span class="sxs-lookup"><span data-stu-id="8d03f-157">b.</span></span> <span data-ttu-id="8d03f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.peoplecart.com`</span><span class="sxs-lookup"><span data-stu-id="8d03f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.peoplecart.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8d03f-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="8d03f-159">These values are not real.</span></span> <span data-ttu-id="8d03f-160">Update these values with the actual Sign-On URL, and Identifier.</span><span class="sxs-lookup"><span data-stu-id="8d03f-160">Update these values with the actual Sign-On URL, and Identifier.</span></span> <span data-ttu-id="8d03f-161">Contact [Peoplecart Client support team](https://peoplecart.com/ContactUs.aspx) to get these values.</span><span class="sxs-lookup"><span data-stu-id="8d03f-161">Contact [Peoplecart Client support team](https://peoplecart.com/ContactUs.aspx) to get these values.</span></span> 
 
1. <span data-ttu-id="8d03f-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8d03f-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/peoplecart-tutorial/tutorial_peoplecart_certificate.png) 

1. <span data-ttu-id="8d03f-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="8d03f-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/peoplecart-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="8d03f-166">On the **Peoplecart Configuration** section, click **Configure Peoplecart** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="8d03f-166">On the **Peoplecart Configuration** section, click **Configure Peoplecart** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8d03f-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="8d03f-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Peoplecart Configuration](./media/peoplecart-tutorial/tutorial_peoplecart_configure.png) 

1. <span data-ttu-id="8d03f-169">To configure single sign-on on **Peoplecart** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Peoplecart support team](https://peoplecart.com/ContactUs.aspx).</span><span class="sxs-lookup"><span data-stu-id="8d03f-169">To configure single sign-on on **Peoplecart** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Peoplecart support team](https://peoplecart.com/ContactUs.aspx).</span></span> <span data-ttu-id="8d03f-170">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="8d03f-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8d03f-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="8d03f-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8d03f-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="8d03f-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8d03f-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8d03f-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8d03f-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8d03f-174">Create an Azure AD test user</span></span>
<span data-ttu-id="8d03f-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d03f-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create an Azure AD test user][100]

<span data-ttu-id="8d03f-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8d03f-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8d03f-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8d03f-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button](./media/peoplecart-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="8d03f-180">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="8d03f-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![The "Users and groups" and "All users" links](./media/peoplecart-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="8d03f-182">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="8d03f-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![The Add button](./media/peoplecart-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="8d03f-184">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8d03f-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![The User dialog box](./media/peoplecart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8d03f-186">a.</span><span class="sxs-lookup"><span data-stu-id="8d03f-186">a.</span></span> <span data-ttu-id="8d03f-187">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8d03f-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8d03f-188">b.</span><span class="sxs-lookup"><span data-stu-id="8d03f-188">b.</span></span> <span data-ttu-id="8d03f-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8d03f-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8d03f-190">c.</span><span class="sxs-lookup"><span data-stu-id="8d03f-190">c.</span></span> <span data-ttu-id="8d03f-191">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="8d03f-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8d03f-192">d.</span><span class="sxs-lookup"><span data-stu-id="8d03f-192">d.</span></span> <span data-ttu-id="8d03f-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8d03f-193">Click **Create**.</span></span>
 
### <a name="create-a-peoplecart-test-user"></a><span data-ttu-id="8d03f-194">Create a Peoplecart test user</span><span class="sxs-lookup"><span data-stu-id="8d03f-194">Create a Peoplecart test user</span></span>

<span data-ttu-id="8d03f-195">In this section, you create a user called Britta Simon in Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="8d03f-195">In this section, you create a user called Britta Simon in Peoplecart.</span></span> <span data-ttu-id="8d03f-196">Work with [Peoplecart support team](https://peoplecart.com/ContactUs.aspx) to add the users in the Peoplecart platform.</span><span class="sxs-lookup"><span data-stu-id="8d03f-196">Work with [Peoplecart support team](https://peoplecart.com/ContactUs.aspx) to add the users in the Peoplecart platform.</span></span> <span data-ttu-id="8d03f-197">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8d03f-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8d03f-198">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8d03f-198">Assign the Azure AD test user</span></span>

<span data-ttu-id="8d03f-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="8d03f-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Peoplecart.</span></span>

![Assign the user role][200] 

<span data-ttu-id="8d03f-201">**To assign Britta Simon to Peoplecart, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8d03f-201">**To assign Britta Simon to Peoplecart, perform the following steps:**</span></span>

1. <span data-ttu-id="8d03f-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8d03f-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="8d03f-204">In the applications list, select **Peoplecart**.</span><span class="sxs-lookup"><span data-stu-id="8d03f-204">In the applications list, select **Peoplecart**.</span></span>

    ![The Peoplecart link in the Applications list](./media/peoplecart-tutorial/tutorial_peoplecart_app.png) 

1. <span data-ttu-id="8d03f-206">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="8d03f-206">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202] 

1. <span data-ttu-id="8d03f-208">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="8d03f-208">Click **Add** button.</span></span> <span data-ttu-id="8d03f-209">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8d03f-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="8d03f-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="8d03f-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="8d03f-212">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="8d03f-212">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="8d03f-213">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8d03f-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8d03f-214">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="8d03f-214">Test single sign-on</span></span>

<span data-ttu-id="8d03f-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8d03f-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8d03f-216">When you click the Peoplecart tile in the Access Panel, you should get login page of Peoplecart application.</span><span class="sxs-lookup"><span data-stu-id="8d03f-216">When you click the Peoplecart tile in the Access Panel, you should get login page of Peoplecart application.</span></span>
<span data-ttu-id="8d03f-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8d03f-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8d03f-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8d03f-218">Additional resources</span></span>

* [<span data-ttu-id="8d03f-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d03f-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="8d03f-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8d03f-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/peoplecart-tutorial/tutorial_general_01.png
[2]: ./media/peoplecart-tutorial/tutorial_general_02.png
[3]: ./media/peoplecart-tutorial/tutorial_general_03.png
[4]: ./media/peoplecart-tutorial/tutorial_general_04.png

[100]: ./media/peoplecart-tutorial/tutorial_general_100.png

[200]: ./media/peoplecart-tutorial/tutorial_general_200.png
[201]: ./media/peoplecart-tutorial/tutorial_general_201.png
[202]: ./media/peoplecart-tutorial/tutorial_general_202.png
[203]: ./media/peoplecart-tutorial/tutorial_general_203.png

