---
title: 'Tutorial: Azure Active Directory integration with Wizergos Productivity Software | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Wizergos Productivity Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/24/2017
ms.author: jeedes
ms.openlocfilehash: 696d0326530baadfffc6f757c2a25690422a12c7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865066"
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="075b0-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="075b0-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>

<span data-ttu-id="075b0-104">In this tutorial, you learn how to integrate Wizergos Productivity Software with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="075b0-104">In this tutorial, you learn how to integrate Wizergos Productivity Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="075b0-105">Integrating Wizergos Productivity Software with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="075b0-105">Integrating Wizergos Productivity Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="075b0-106">You can control in Azure AD who has access to Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="075b0-106">You can control in Azure AD who has access to Wizergos Productivity Software.</span></span>
- <span data-ttu-id="075b0-107">You can enable your users to automatically get signed-on to Wizergos Productivity Software (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="075b0-107">You can enable your users to automatically get signed-on to Wizergos Productivity Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="075b0-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="075b0-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="075b0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="075b0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="075b0-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="075b0-110">Prerequisites</span></span>

<span data-ttu-id="075b0-111">To configure Azure AD integration with Wizergos Productivity Software, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="075b0-111">To configure Azure AD integration with Wizergos Productivity Software, you need the following items:</span></span>

- <span data-ttu-id="075b0-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="075b0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="075b0-113">A Wizergos Productivity Software single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="075b0-113">A Wizergos Productivity Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="075b0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="075b0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="075b0-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="075b0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="075b0-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="075b0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="075b0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="075b0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="075b0-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="075b0-118">Scenario description</span></span>
<span data-ttu-id="075b0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="075b0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="075b0-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="075b0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="075b0-121">Adding Wizergos Productivity Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="075b0-121">Adding Wizergos Productivity Software from the gallery</span></span>
1. <span data-ttu-id="075b0-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="075b0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wizergos-productivity-software-from-the-gallery"></a><span data-ttu-id="075b0-123">Adding Wizergos Productivity Software from the gallery</span><span class="sxs-lookup"><span data-stu-id="075b0-123">Adding Wizergos Productivity Software from the gallery</span></span>
<span data-ttu-id="075b0-124">To configure the integration of Wizergos Productivity Software into Azure AD, you need to add Wizergos Productivity Software from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="075b0-124">To configure the integration of Wizergos Productivity Software into Azure AD, you need to add Wizergos Productivity Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="075b0-125">**To add Wizergos Productivity Software from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="075b0-125">**To add Wizergos Productivity Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="075b0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="075b0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="075b0-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="075b0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="075b0-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="075b0-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="075b0-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="075b0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="075b0-133">In the search box, type **Wizergos Productivity Software**, select **Wizergos Productivity Software** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="075b0-133">In the search box, type **Wizergos Productivity Software**, select **Wizergos Productivity Software** from result panel then click **Add** button to add the application.</span></span>

    ![Wizergos Productivity Software in the results list](./media/wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="075b0-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="075b0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="075b0-136">In this section, you configure and test Azure AD single sign-on with Wizergos Productivity Software based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="075b0-136">In this section, you configure and test Azure AD single sign-on with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="075b0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Wizergos Productivity Software is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="075b0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Wizergos Productivity Software is to a user in Azure AD.</span></span> <span data-ttu-id="075b0-138">In other words, a link relationship between an Azure AD user and the related user in Wizergos Productivity Software needs to be established.</span><span class="sxs-lookup"><span data-stu-id="075b0-138">In other words, a link relationship between an Azure AD user and the related user in Wizergos Productivity Software needs to be established.</span></span>

<span data-ttu-id="075b0-139">In Wizergos Productivity Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="075b0-139">In Wizergos Productivity Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="075b0-140">To configure and test Azure AD single sign-on with Wizergos Productivity Software, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="075b0-140">To configure and test Azure AD single sign-on with Wizergos Productivity Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="075b0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="075b0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="075b0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="075b0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="075b0-143">**[Create a Wizergos Productivity Software test user](#create-a-wizergos-productivity-software-test-user)** - to have a counterpart of Britta Simon in Wizergos Productivity Software that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="075b0-143">**[Create a Wizergos Productivity Software test user](#create-a-wizergos-productivity-software-test-user)** - to have a counterpart of Britta Simon in Wizergos Productivity Software that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="075b0-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="075b0-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="075b0-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="075b0-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="075b0-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="075b0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="075b0-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wizergos Productivity Software application.</span><span class="sxs-lookup"><span data-stu-id="075b0-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="075b0-148">**To configure Azure AD single sign-on with Wizergos Productivity Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="075b0-148">**To configure Azure AD single sign-on with Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="075b0-149">In the Azure portal, on the **Wizergos Productivity Software** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="075b0-149">In the Azure portal, on the **Wizergos Productivity Software** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="075b0-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="075b0-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_samlbase.png)

1. <span data-ttu-id="075b0-153">On the **Wizergos Productivity Software Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="075b0-153">On the **Wizergos Productivity Software Domain and URLs** section, perform the following steps:</span></span>

    ![Wizergos Productivity Software Domain and URLs single sign-on information](./media/wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_url.png)

    <span data-ttu-id="075b0-155">In the **Identifier** textbox, type the URL: `http://www.wizergos.net`</span><span class="sxs-lookup"><span data-stu-id="075b0-155">In the **Identifier** textbox, type the URL: `http://www.wizergos.net`</span></span>

1. <span data-ttu-id="075b0-156">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="075b0-156">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_certificate.png) 

1. <span data-ttu-id="075b0-158">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="075b0-158">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/wizergosproductivitysoftware-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="075b0-160">On the **Wizergos Productivity Software Configuration** section, click **Configure Wizergos Productivity Software** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="075b0-160">On the **Wizergos Productivity Software Configuration** section, click **Configure Wizergos Productivity Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="075b0-161">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="075b0-161">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Wizergos Productivity Software Configuration](./media/wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_configure.png) 

1. <span data-ttu-id="075b0-163">In a different web browser window, sign-on to your Wizergos Productivity Software tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="075b0-163">In a different web browser window, sign-on to your Wizergos Productivity Software tenant as an administrator.</span></span>

1. <span data-ttu-id="075b0-164">From the hamburger menu, select **Admin**.</span><span class="sxs-lookup"><span data-stu-id="075b0-164">From the hamburger menu, select **Admin**.</span></span>

    ![Configure Single Sign-On On App side](./media/wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)

1. <span data-ttu-id="075b0-166">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="075b0-166">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>

    ![Configure Single Sign-On On App side](./media/wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)

1. <span data-ttu-id="075b0-168">Perform the following steps on **AUTHENTICATION** section.</span><span class="sxs-lookup"><span data-stu-id="075b0-168">Perform the following steps on **AUTHENTICATION** section.</span></span>

    ![Configure Single Sign-On On App side](./media/wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
    
    <span data-ttu-id="075b0-170">a.</span><span class="sxs-lookup"><span data-stu-id="075b0-170">a.</span></span> <span data-ttu-id="075b0-171">Click **UPLOAD** button to upload the downloaded certificate from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="075b0-171">Click **UPLOAD** button to upload the downloaded certificate from Azure AD.</span></span>
    
    <span data-ttu-id="075b0-172">b.</span><span class="sxs-lookup"><span data-stu-id="075b0-172">b.</span></span> <span data-ttu-id="075b0-173">In the **Issuer URL** textbox, paste the **SAML Entity ID** value which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="075b0-173">In the **Issuer URL** textbox, paste the **SAML Entity ID** value which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="075b0-174">c.</span><span class="sxs-lookup"><span data-stu-id="075b0-174">c.</span></span> <span data-ttu-id="075b0-175">In the **Single Sign-On URL** textbox, paste the **SAML Single Sign-On Service URL** value which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="075b0-175">In the **Single Sign-On URL** textbox, paste the **SAML Single Sign-On Service URL** value which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="075b0-176">d.</span><span class="sxs-lookup"><span data-stu-id="075b0-176">d.</span></span> <span data-ttu-id="075b0-177">In the **Single Sign-Out URL** textbox, paste the **Sign-Out URL** value which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="075b0-177">In the **Single Sign-Out URL** textbox, paste the **Sign-Out URL** value which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="075b0-178">e.</span><span class="sxs-lookup"><span data-stu-id="075b0-178">e.</span></span> <span data-ttu-id="075b0-179">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="075b0-179">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="075b0-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="075b0-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="075b0-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="075b0-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="075b0-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="075b0-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="075b0-183">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="075b0-183">Create an Azure AD test user</span></span>

<span data-ttu-id="075b0-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="075b0-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="075b0-186">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="075b0-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="075b0-187">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="075b0-187">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/wizergosproductivitysoftware-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="075b0-189">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="075b0-189">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/wizergosproductivitysoftware-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="075b0-191">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="075b0-191">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/wizergosproductivitysoftware-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="075b0-193">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="075b0-193">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/wizergosproductivitysoftware-tutorial/create_aaduser_04.png)

    <span data-ttu-id="075b0-195">a.</span><span class="sxs-lookup"><span data-stu-id="075b0-195">a.</span></span> <span data-ttu-id="075b0-196">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="075b0-196">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="075b0-197">b.</span><span class="sxs-lookup"><span data-stu-id="075b0-197">b.</span></span> <span data-ttu-id="075b0-198">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="075b0-198">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="075b0-199">c.</span><span class="sxs-lookup"><span data-stu-id="075b0-199">c.</span></span> <span data-ttu-id="075b0-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="075b0-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="075b0-201">d.</span><span class="sxs-lookup"><span data-stu-id="075b0-201">d.</span></span> <span data-ttu-id="075b0-202">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="075b0-202">Click **Create**.</span></span>
 
### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="075b0-203">Create a Wizergos Productivity Software test user</span><span class="sxs-lookup"><span data-stu-id="075b0-203">Create a Wizergos Productivity Software test user</span></span>

<span data-ttu-id="075b0-204">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="075b0-204">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="075b0-205">Please work with [Wizergos Productivity Software support team](mailTo:support@wizergos.com) to add the users in the Wizergos Productivity Software platform.</span><span class="sxs-lookup"><span data-stu-id="075b0-205">Please work with [Wizergos Productivity Software support team](mailTo:support@wizergos.com) to add the users in the Wizergos Productivity Software platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="075b0-206">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="075b0-206">Assign the Azure AD test user</span></span>

<span data-ttu-id="075b0-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="075b0-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wizergos Productivity Software.</span></span>

![Assign the user role][200] 

<span data-ttu-id="075b0-209">**To assign Britta Simon to Wizergos Productivity Software, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="075b0-209">**To assign Britta Simon to Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="075b0-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="075b0-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="075b0-212">In the applications list, select **Wizergos Productivity Software**.</span><span class="sxs-lookup"><span data-stu-id="075b0-212">In the applications list, select **Wizergos Productivity Software**.</span></span>

    ![The Wizergos Productivity Software link in the Applications list](./media/wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_app.png)  

1. <span data-ttu-id="075b0-214">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="075b0-214">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="075b0-216">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="075b0-216">Click **Add** button.</span></span> <span data-ttu-id="075b0-217">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="075b0-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="075b0-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="075b0-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="075b0-220">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="075b0-220">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="075b0-221">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="075b0-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="075b0-222">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="075b0-222">Test single sign-on</span></span>

<span data-ttu-id="075b0-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="075b0-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="075b0-224">When you click the Wizergos Productivity Software tile in the Access Panel, you should get automatically signed-on to your Wizergos Productivity Software application.</span><span class="sxs-lookup"><span data-stu-id="075b0-224">When you click the Wizergos Productivity Software tile in the Access Panel, you should get automatically signed-on to your Wizergos Productivity Software application.</span></span>
<span data-ttu-id="075b0-225">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="075b0-225">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="075b0-226">Additional resources</span><span class="sxs-lookup"><span data-stu-id="075b0-226">Additional resources</span></span>

* [<span data-ttu-id="075b0-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="075b0-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="075b0-228">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="075b0-228">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[100]: ./media/wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[202]: ./media/wizergosproductivitysoftware-tutorial/tutorial_general_202.png
[203]: ./media/wizergosproductivitysoftware-tutorial/tutorial_general_203.png

