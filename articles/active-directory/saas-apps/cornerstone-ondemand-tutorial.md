---
title: 'Tutorial: Azure Active Directory integration with Cornerstone OnDemand | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Cornerstone OnDemand.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: f57c5fef-49b0-4591-91ef-fc0de6d654ab
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jeedes
ms.openlocfilehash: 4927421afeddc337856c027b3ed32539f4f8c1fc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856591"
---
# <a name="tutorial-azure-active-directory-integration-with-cornerstone-ondemand"></a><span data-ttu-id="9211d-103">Tutorial: Azure Active Directory integration with Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="9211d-103">Tutorial: Azure Active Directory integration with Cornerstone OnDemand</span></span>

<span data-ttu-id="9211d-104">In this tutorial, you learn how to integrate Cornerstone OnDemand with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9211d-104">In this tutorial, you learn how to integrate Cornerstone OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9211d-105">Integrating Cornerstone OnDemand with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="9211d-105">Integrating Cornerstone OnDemand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9211d-106">You can control in Azure AD who has access to Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="9211d-106">You can control in Azure AD who has access to Cornerstone OnDemand</span></span>
- <span data-ttu-id="9211d-107">You can enable your users to automatically get signed-on to Cornerstone OnDemand (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="9211d-107">You can enable your users to automatically get signed-on to Cornerstone OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9211d-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="9211d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9211d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="9211d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9211d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9211d-110">Prerequisites</span></span>

<span data-ttu-id="9211d-111">To configure Azure AD integration with Cornerstone OnDemand, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="9211d-111">To configure Azure AD integration with Cornerstone OnDemand, you need the following items:</span></span>

- <span data-ttu-id="9211d-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="9211d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9211d-113">A Cornerstone OnDemand single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="9211d-113">A Cornerstone OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9211d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="9211d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9211d-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="9211d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9211d-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="9211d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9211d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9211d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9211d-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="9211d-118">Scenario description</span></span>
<span data-ttu-id="9211d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="9211d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9211d-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="9211d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9211d-121">Adding Cornerstone OnDemand from the gallery</span><span class="sxs-lookup"><span data-stu-id="9211d-121">Adding Cornerstone OnDemand from the gallery</span></span>
1. <span data-ttu-id="9211d-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9211d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cornerstone-ondemand-from-the-gallery"></a><span data-ttu-id="9211d-123">Adding Cornerstone OnDemand from the gallery</span><span class="sxs-lookup"><span data-stu-id="9211d-123">Adding Cornerstone OnDemand from the gallery</span></span>
<span data-ttu-id="9211d-124">To configure the integration of Cornerstone OnDemand into Azure AD, you need to add Cornerstone OnDemand from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="9211d-124">To configure the integration of Cornerstone OnDemand into Azure AD, you need to add Cornerstone OnDemand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9211d-125">**To add Cornerstone OnDemand from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9211d-125">**To add Cornerstone OnDemand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9211d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9211d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="9211d-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="9211d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9211d-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9211d-129">Then go to **All applications**.</span></span>

    ![Applications][2]

1. <span data-ttu-id="9211d-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="9211d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="9211d-133">In the search box, type **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="9211d-133">In the search box, type **Cornerstone OnDemand**.</span></span>

    ![Creating an Azure AD test user](./media/cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_search.png)

1. <span data-ttu-id="9211d-135">In the results panel, select **Cornerstone OnDemand**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="9211d-135">In the results panel, select **Cornerstone OnDemand**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9211d-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9211d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9211d-138">In this section, you configure and test Azure AD single sign-on with Cornerstone OnDemand based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="9211d-138">In this section, you configure and test Azure AD single sign-on with Cornerstone OnDemand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9211d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cornerstone OnDemand is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9211d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cornerstone OnDemand is to a user in Azure AD.</span></span> <span data-ttu-id="9211d-140">In other words, a link relationship between an Azure AD user and the related user in Cornerstone OnDemand needs to be established.</span><span class="sxs-lookup"><span data-stu-id="9211d-140">In other words, a link relationship between an Azure AD user and the related user in Cornerstone OnDemand needs to be established.</span></span>

<span data-ttu-id="9211d-141">In Cornerstone OnDemand, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="9211d-141">In Cornerstone OnDemand, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9211d-142">To configure and test Azure AD single sign-on with Cornerstone OnDemand, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="9211d-142">To configure and test Azure AD single sign-on with Cornerstone OnDemand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9211d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="9211d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="9211d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9211d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="9211d-145">**[Creating a Cornerstone OnDemand test user](#creating-a-cornerstone-ondemand-test-user)** - to have a counterpart of Britta Simon in Cornerstone OnDemand that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="9211d-145">**[Creating a Cornerstone OnDemand test user](#creating-a-cornerstone-ondemand-test-user)** - to have a counterpart of Britta Simon in Cornerstone OnDemand that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="9211d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9211d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="9211d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="9211d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9211d-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9211d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9211d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cornerstone OnDemand application.</span><span class="sxs-lookup"><span data-stu-id="9211d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cornerstone OnDemand application.</span></span>

<span data-ttu-id="9211d-150">**To configure Azure AD single sign-on with Cornerstone OnDemand, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9211d-150">**To configure Azure AD single sign-on with Cornerstone OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="9211d-151">In the Azure portal, on the **Cornerstone OnDemand** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9211d-151">In the Azure portal, on the **Cornerstone OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="9211d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9211d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configure Single Sign-On](./media/cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_samlbase.png)

1. <span data-ttu-id="9211d-155">On the **Cornerstone OnDemand Domain and URLs** section, perform the following step:</span><span class="sxs-lookup"><span data-stu-id="9211d-155">On the **Cornerstone OnDemand Domain and URLs** section, perform the following step:</span></span>

    ![Configure Single Sign-On](./media/cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_url.png)

    <span data-ttu-id="9211d-157">a.</span><span class="sxs-lookup"><span data-stu-id="9211d-157">a.</span></span> <span data-ttu-id="9211d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="9211d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.csod.com`</span></span>

    <span data-ttu-id="9211d-159">b.</span><span class="sxs-lookup"><span data-stu-id="9211d-159">b.</span></span> <span data-ttu-id="9211d-160">In **Identifier** textbox, type a URL using the following pattern: `https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="9211d-160">In **Identifier** textbox, type a URL using the following pattern: `https://<company>.csod.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9211d-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="9211d-161">These values are not real.</span></span> <span data-ttu-id="9211d-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="9211d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9211d-163">Contact [Cornerstone OnDemand Client support team](mailTo:moreinfo@csod.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="9211d-163">Contact [Cornerstone OnDemand Client support team](mailTo:moreinfo@csod.com) to get these values.</span></span>

1. <span data-ttu-id="9211d-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="9211d-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_certificate.png) 

1. <span data-ttu-id="9211d-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="9211d-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/cornerstone-ondemand-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="9211d-168">On the **Cornerstone OnDemand Configuration** section, click **Configure Cornerstone OnDemand** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="9211d-168">On the **Cornerstone OnDemand Configuration** section, click **Configure Cornerstone OnDemand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9211d-169">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="9211d-169">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_configure.png) 

1. <span data-ttu-id="9211d-171">To configure single sign-on on **Cornerstone OnDemand** side, you need to send the downloaded **Certificate**, **Sign-Out URL** and **SAML Single Sign-On Service URL**  to [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="9211d-171">To configure single sign-on on **Cornerstone OnDemand** side, you need to send the downloaded **Certificate**, **Sign-Out URL** and **SAML Single Sign-On Service URL**  to [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span> <span data-ttu-id="9211d-172">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="9211d-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9211d-173">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9211d-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="9211d-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9211d-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="9211d-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9211d-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9211d-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9211d-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/cornerstone-ondemand-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="9211d-179">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="9211d-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>

    ![Creating an Azure AD test user](./media/cornerstone-ondemand-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="9211d-181">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="9211d-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>

    ![Creating an Azure AD test user](./media/cornerstone-ondemand-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="9211d-183">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9211d-183">On the **User** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](./media/cornerstone-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9211d-185">a.</span><span class="sxs-lookup"><span data-stu-id="9211d-185">a.</span></span> <span data-ttu-id="9211d-186">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9211d-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9211d-187">b.</span><span class="sxs-lookup"><span data-stu-id="9211d-187">b.</span></span> <span data-ttu-id="9211d-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9211d-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9211d-189">c.</span><span class="sxs-lookup"><span data-stu-id="9211d-189">c.</span></span> <span data-ttu-id="9211d-190">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="9211d-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9211d-191">d.</span><span class="sxs-lookup"><span data-stu-id="9211d-191">d.</span></span> <span data-ttu-id="9211d-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="9211d-192">Click **Create**.</span></span>

### <a name="creating-a-cornerstone-ondemand-test-user"></a><span data-ttu-id="9211d-193">Creating a Cornerstone OnDemand test user</span><span class="sxs-lookup"><span data-stu-id="9211d-193">Creating a Cornerstone OnDemand test user</span></span>

<span data-ttu-id="9211d-194">The objective of this section is to create a user called Britta Simon in Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="9211d-194">The objective of this section is to create a user called Britta Simon in Cornerstone OnDemand.</span></span> <span data-ttu-id="9211d-195">Cornerstone OnDemand supports automatic user provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="9211d-195">Cornerstone OnDemand supports automatic user provisioning, which is by default enabled.</span></span> <span data-ttu-id="9211d-196">You can find more details [here](cornerstone-ondemand-provisioning-tutorial.md) on how to configure automatic user provisioning.</span><span class="sxs-lookup"><span data-stu-id="9211d-196">You can find more details [here](cornerstone-ondemand-provisioning-tutorial.md) on how to configure automatic user provisioning.</span></span>

<span data-ttu-id="9211d-197">**If you need to create user manually, perform following steps:**</span><span class="sxs-lookup"><span data-stu-id="9211d-197">**If you need to create user manually, perform following steps:**</span></span>

<span data-ttu-id="9211d-198">To configure user provisioning, send the information (e.g.: Name, Email) about the Azure AD user you want to provision to the [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="9211d-198">To configure user provisioning, send the information (e.g.: Name, Email) about the Azure AD user you want to provision to the [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span>

>[!NOTE]
><span data-ttu-id="9211d-199">You can use any other Cornerstone OnDemand user account creation tools or APIs provided by Cornerstone OnDemand to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="9211d-199">You can use any other Cornerstone OnDemand user account creation tools or APIs provided by Cornerstone OnDemand to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9211d-200">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9211d-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9211d-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="9211d-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cornerstone OnDemand.</span></span>

![Assign User][200] 

<span data-ttu-id="9211d-203">**To assign Britta Simon to Cornerstone OnDemand, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9211d-203">**To assign Britta Simon to Cornerstone OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="9211d-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9211d-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="9211d-206">In the applications list, select **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="9211d-206">In the applications list, select **Cornerstone OnDemand**.</span></span>

    ![Configure Single Sign-On](./media/cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_app.png) 

1. <span data-ttu-id="9211d-208">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="9211d-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="9211d-210">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="9211d-210">Click **Add** button.</span></span> <span data-ttu-id="9211d-211">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9211d-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="9211d-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="9211d-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="9211d-214">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="9211d-214">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="9211d-215">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9211d-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9211d-216">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="9211d-216">Testing single sign-on</span></span>

<span data-ttu-id="9211d-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9211d-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9211d-218">When you click the Cornerstone OnDemand tile in the Access Panel, you should get automatically signed-on to your Cornerstone OnDemand application.</span><span class="sxs-lookup"><span data-stu-id="9211d-218">When you click the Cornerstone OnDemand tile in the Access Panel, you should get automatically signed-on to your Cornerstone OnDemand application.</span></span>
<span data-ttu-id="9211d-219">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9211d-219">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9211d-220">Additional resources</span><span class="sxs-lookup"><span data-stu-id="9211d-220">Additional resources</span></span>

* [<span data-ttu-id="9211d-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9211d-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="9211d-222">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9211d-222">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="9211d-223">Configure User Provisioning</span><span class="sxs-lookup"><span data-stu-id="9211d-223">Configure User Provisioning</span></span>](cornerstone-ondemand-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/cornerstone-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/cornerstone-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/cornerstone-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/cornerstone-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/cornerstone-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/cornerstone-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/cornerstone-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/cornerstone-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/cornerstone-ondemand-tutorial/tutorial_general_203.png
