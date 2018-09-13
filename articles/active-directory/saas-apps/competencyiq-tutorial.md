---
title: 'Tutorial: Azure Active Directory integration with CompetencyIQ | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and CompetencyIQ.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: e262bf7e-cc7d-4d0e-aea7-861f00d8837d
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 8cb474c56e1802ccfe828f0040ae231f0748551e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966168"
---
# <a name="tutorial-azure-active-directory-integration-with-competencyiq"></a><span data-ttu-id="f0345-103">Tutorial: Azure Active Directory integration with CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="f0345-103">Tutorial: Azure Active Directory integration with CompetencyIQ</span></span>

<span data-ttu-id="f0345-104">In this tutorial, you learn how to integrate CompetencyIQ with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f0345-104">In this tutorial, you learn how to integrate CompetencyIQ with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f0345-105">Integrating CompetencyIQ with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f0345-105">Integrating CompetencyIQ with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f0345-106">You can control in Azure AD who has access to CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="f0345-106">You can control in Azure AD who has access to CompetencyIQ</span></span>
- <span data-ttu-id="f0345-107">You can enable your users to automatically get signed-on to CompetencyIQ (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="f0345-107">You can enable your users to automatically get signed-on to CompetencyIQ (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f0345-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f0345-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f0345-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="f0345-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0345-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f0345-110">Prerequisites</span></span>

<span data-ttu-id="f0345-111">To configure Azure AD integration with CompetencyIQ, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f0345-111">To configure Azure AD integration with CompetencyIQ, you need the following items:</span></span>

- <span data-ttu-id="f0345-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f0345-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f0345-113">A CompetencyIQ single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f0345-113">A CompetencyIQ single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f0345-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f0345-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f0345-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f0345-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f0345-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="f0345-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f0345-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f0345-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f0345-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f0345-118">Scenario description</span></span>
<span data-ttu-id="f0345-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f0345-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f0345-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f0345-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f0345-121">Adding CompetencyIQ from the gallery</span><span class="sxs-lookup"><span data-stu-id="f0345-121">Adding CompetencyIQ from the gallery</span></span>
1. <span data-ttu-id="f0345-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f0345-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-competencyiq-from-the-gallery"></a><span data-ttu-id="f0345-123">Adding CompetencyIQ from the gallery</span><span class="sxs-lookup"><span data-stu-id="f0345-123">Adding CompetencyIQ from the gallery</span></span>
<span data-ttu-id="f0345-124">To configure the integration of CompetencyIQ into Azure AD, you need to add CompetencyIQ from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f0345-124">To configure the integration of CompetencyIQ into Azure AD, you need to add CompetencyIQ from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f0345-125">**To add CompetencyIQ from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f0345-125">**To add CompetencyIQ from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f0345-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f0345-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="f0345-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="f0345-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f0345-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f0345-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="f0345-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="f0345-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="f0345-133">In the search box, type **CompetencyIQ**.</span><span class="sxs-lookup"><span data-stu-id="f0345-133">In the search box, type **CompetencyIQ**.</span></span>

    ![Creating an Azure AD test user](./media/competencyiq-tutorial/tutorial_competencyiq_search.png)

1. <span data-ttu-id="f0345-135">In the results panel, select **CompetencyIQ**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="f0345-135">In the results panel, select **CompetencyIQ**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/competencyiq-tutorial/tutorial_competencyiq_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f0345-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f0345-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f0345-138">In this section, you configure and test Azure AD single sign-on with CompetencyIQ based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="f0345-138">In this section, you configure and test Azure AD single sign-on with CompetencyIQ based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f0345-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CompetencyIQ is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0345-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CompetencyIQ is to a user in Azure AD.</span></span> <span data-ttu-id="f0345-140">In other words, a link relationship between an Azure AD user and the related user in CompetencyIQ needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f0345-140">In other words, a link relationship between an Azure AD user and the related user in CompetencyIQ needs to be established.</span></span>

<span data-ttu-id="f0345-141">In CompetencyIQ, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="f0345-141">In CompetencyIQ, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f0345-142">To configure and test Azure AD single sign-on with CompetencyIQ, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f0345-142">To configure and test Azure AD single sign-on with CompetencyIQ, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f0345-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f0345-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="f0345-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f0345-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="f0345-145">**[Creating a CompetencyIQ test user](#creating-a-competencyiq-test-user)** - to have a counterpart of Britta Simon in CompetencyIQ that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="f0345-145">**[Creating a CompetencyIQ test user](#creating-a-competencyiq-test-user)** - to have a counterpart of Britta Simon in CompetencyIQ that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="f0345-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f0345-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="f0345-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f0345-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f0345-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f0345-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f0345-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CompetencyIQ application.</span><span class="sxs-lookup"><span data-stu-id="f0345-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CompetencyIQ application.</span></span>

<span data-ttu-id="f0345-150">**To configure Azure AD single sign-on with CompetencyIQ, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f0345-150">**To configure Azure AD single sign-on with CompetencyIQ, perform the following steps:**</span></span>

1. <span data-ttu-id="f0345-151">In the Azure portal, on the **CompetencyIQ** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f0345-151">In the Azure portal, on the **CompetencyIQ** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="f0345-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f0345-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/competencyiq-tutorial/tutorial_competencyiq_samlbase.png)

1. <span data-ttu-id="f0345-155">On the **CompetencyIQ Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f0345-155">On the **CompetencyIQ Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/competencyiq-tutorial/tutorial_competencyiq_url1.png)

    <span data-ttu-id="f0345-157">a.</span><span class="sxs-lookup"><span data-stu-id="f0345-157">a.</span></span> <span data-ttu-id="f0345-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<customer>.competencyiq.com/`</span><span class="sxs-lookup"><span data-stu-id="f0345-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<customer>.competencyiq.com/`</span></span>
    
    <span data-ttu-id="f0345-159">b.</span><span class="sxs-lookup"><span data-stu-id="f0345-159">b.</span></span> <span data-ttu-id="f0345-160">In the **Identifier** textbox, type the URL: `https://www.competencyiq.com/`</span><span class="sxs-lookup"><span data-stu-id="f0345-160">In the **Identifier** textbox, type the URL: `https://www.competencyiq.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f0345-161">The Sign-on URL value is not real so update this with actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="f0345-161">The Sign-on URL value is not real so update this with actual Sign-On URL.</span></span> <span data-ttu-id="f0345-162">Contact [CompetencyIQ Client support team](https://www.competencyiq.com/) to get this.</span><span class="sxs-lookup"><span data-stu-id="f0345-162">Contact [CompetencyIQ Client support team](https://www.competencyiq.com/) to get this.</span></span> 
 
1. <span data-ttu-id="f0345-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="f0345-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/competencyiq-tutorial/tutorial_competencyiq_certificate.png) 

1. <span data-ttu-id="f0345-165">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="f0345-165">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/competencyiq-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="f0345-167">On the **CompetencyIQ Configuration** section, click **Configure CompetencyIQ** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="f0345-167">On the **CompetencyIQ Configuration** section, click **Configure CompetencyIQ** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f0345-168">Copy the **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="f0345-168">Copy the **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/competencyiq-tutorial/tutorial_competencyiq_configure.png) 

1. <span data-ttu-id="f0345-170">To configure single sign-on on **CompetencyIQ** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [CompetencyIQ support team](https://www.competencyiq.com/).</span><span class="sxs-lookup"><span data-stu-id="f0345-170">To configure single sign-on on **CompetencyIQ** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [CompetencyIQ support team](https://www.competencyiq.com/).</span></span> <span data-ttu-id="f0345-171">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="f0345-171">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f0345-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="f0345-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f0345-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="f0345-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f0345-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f0345-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f0345-175">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f0345-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="f0345-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f0345-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="f0345-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f0345-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f0345-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f0345-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/competencyiq-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="f0345-181">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="f0345-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/competencyiq-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="f0345-183">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="f0345-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/competencyiq-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="f0345-185">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f0345-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/competencyiq-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f0345-187">a.</span><span class="sxs-lookup"><span data-stu-id="f0345-187">a.</span></span> <span data-ttu-id="f0345-188">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f0345-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f0345-189">b.</span><span class="sxs-lookup"><span data-stu-id="f0345-189">b.</span></span> <span data-ttu-id="f0345-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f0345-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f0345-191">c.</span><span class="sxs-lookup"><span data-stu-id="f0345-191">c.</span></span> <span data-ttu-id="f0345-192">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="f0345-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f0345-193">d.</span><span class="sxs-lookup"><span data-stu-id="f0345-193">d.</span></span> <span data-ttu-id="f0345-194">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f0345-194">Click **Create**.</span></span>
 
### <a name="creating-a-competencyiq-test-user"></a><span data-ttu-id="f0345-195">Creating a CompetencyIQ test user</span><span class="sxs-lookup"><span data-stu-id="f0345-195">Creating a CompetencyIQ test user</span></span>

<span data-ttu-id="f0345-196">To enable Azure AD users to log in to CompetencyIQ, they must be provisioned into CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="f0345-196">To enable Azure AD users to log in to CompetencyIQ, they must be provisioned into CompetencyIQ.</span></span> <span data-ttu-id="f0345-197">Contact [CompetencyIQ support team](https://www.competencyiq.com/) to create users in the application.</span><span class="sxs-lookup"><span data-stu-id="f0345-197">Contact [CompetencyIQ support team](https://www.competencyiq.com/) to create users in the application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f0345-198">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f0345-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f0345-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="f0345-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CompetencyIQ.</span></span>

![Assign User][200] 

<span data-ttu-id="f0345-201">**To assign Britta Simon to CompetencyIQ, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f0345-201">**To assign Britta Simon to CompetencyIQ, perform the following steps:**</span></span>

1. <span data-ttu-id="f0345-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f0345-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="f0345-204">In the applications list, select **CompetencyIQ**.</span><span class="sxs-lookup"><span data-stu-id="f0345-204">In the applications list, select **CompetencyIQ**.</span></span>

    ![Configure Single Sign-On](./media/competencyiq-tutorial/tutorial_competencyiq_app.png) 

1. <span data-ttu-id="f0345-206">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f0345-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="f0345-208">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="f0345-208">Click **Add** button.</span></span> <span data-ttu-id="f0345-209">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f0345-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="f0345-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="f0345-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="f0345-212">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="f0345-212">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="f0345-213">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f0345-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f0345-214">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="f0345-214">Testing single sign-on</span></span>

<span data-ttu-id="f0345-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f0345-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f0345-216">When you click the CompetencyIQ tile in the Access Panel, you should get automatically logged into the application.</span><span class="sxs-lookup"><span data-stu-id="f0345-216">When you click the CompetencyIQ tile in the Access Panel, you should get automatically logged into the application.</span></span>
<span data-ttu-id="f0345-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f0345-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f0345-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f0345-218">Additional resources</span></span>

* [<span data-ttu-id="f0345-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0345-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="f0345-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f0345-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/competencyiq-tutorial/tutorial_general_01.png
[2]: ./media/competencyiq-tutorial/tutorial_general_02.png
[3]: ./media/competencyiq-tutorial/tutorial_general_03.png
[4]: ./media/competencyiq-tutorial/tutorial_general_04.png

[100]: ./media/competencyiq-tutorial/tutorial_general_100.png

[200]: ./media/competencyiq-tutorial/tutorial_general_200.png
[201]: ./media/competencyiq-tutorial/tutorial_general_201.png
[202]: ./media/competencyiq-tutorial/tutorial_general_202.png
[203]: ./media/competencyiq-tutorial/tutorial_general_203.png

