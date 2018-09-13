---
title: 'Tutorial: Azure Active Directory integration with Tango Analytics | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Tango Analytics.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 2f7555d3-e9ba-40b2-9b3a-2f0ab38a4c08
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: eb0e309eed5594f806a65bc3f2820cdb9a861309
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867801"
---
# <a name="tutorial-azure-active-directory-integration-with-tango-analytics"></a><span data-ttu-id="cc1af-103">Tutorial: Azure Active Directory integration with Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="cc1af-103">Tutorial: Azure Active Directory integration with Tango Analytics</span></span>

<span data-ttu-id="cc1af-104">In this tutorial, you learn how to integrate Tango Analytics with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc1af-104">In this tutorial, you learn how to integrate Tango Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc1af-105">Integrating Tango Analytics with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="cc1af-105">Integrating Tango Analytics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cc1af-106">You can control in Azure AD who has access to Tango Analytics</span><span class="sxs-lookup"><span data-stu-id="cc1af-106">You can control in Azure AD who has access to Tango Analytics</span></span>
- <span data-ttu-id="cc1af-107">You can enable your users to automatically get signed-on to Tango Analytics (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="cc1af-107">You can enable your users to automatically get signed-on to Tango Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cc1af-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="cc1af-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cc1af-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="cc1af-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc1af-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cc1af-110">Prerequisites</span></span>

<span data-ttu-id="cc1af-111">To configure Azure AD integration with Tango Analytics, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="cc1af-111">To configure Azure AD integration with Tango Analytics, you need the following items:</span></span>

- <span data-ttu-id="cc1af-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="cc1af-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc1af-113">A Tango Analytics single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="cc1af-113">A Tango Analytics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc1af-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="cc1af-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc1af-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="cc1af-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc1af-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="cc1af-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc1af-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc1af-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc1af-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="cc1af-118">Scenario description</span></span>
<span data-ttu-id="cc1af-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="cc1af-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc1af-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="cc1af-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc1af-121">Adding Tango Analytics from the gallery</span><span class="sxs-lookup"><span data-stu-id="cc1af-121">Adding Tango Analytics from the gallery</span></span>
1. <span data-ttu-id="cc1af-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cc1af-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tango-analytics-from-the-gallery"></a><span data-ttu-id="cc1af-123">Adding Tango Analytics from the gallery</span><span class="sxs-lookup"><span data-stu-id="cc1af-123">Adding Tango Analytics from the gallery</span></span>
<span data-ttu-id="cc1af-124">To configure the integration of Tango Analytics into Azure AD, you need to add Tango Analytics from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="cc1af-124">To configure the integration of Tango Analytics into Azure AD, you need to add Tango Analytics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cc1af-125">**To add Tango Analytics from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cc1af-125">**To add Tango Analytics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cc1af-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="cc1af-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="cc1af-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="cc1af-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cc1af-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cc1af-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="cc1af-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="cc1af-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="cc1af-133">In the search box, type **Tango Analytics**.</span><span class="sxs-lookup"><span data-stu-id="cc1af-133">In the search box, type **Tango Analytics**.</span></span>

    ![Creating an Azure AD test user](./media/tangoanalytics-tutorial/tutorial_tangoanalytics_search.png)

1. <span data-ttu-id="cc1af-135">In the results panel, select **Tango Analytics**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="cc1af-135">In the results panel, select **Tango Analytics**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/tangoanalytics-tutorial/tutorial_tangoanalytics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cc1af-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cc1af-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cc1af-138">In this section, you configure and test Azure AD single sign-on with Tango Analytics based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cc1af-138">In this section, you configure and test Azure AD single sign-on with Tango Analytics based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cc1af-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tango Analytics is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc1af-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tango Analytics is to a user in Azure AD.</span></span> <span data-ttu-id="cc1af-140">In other words, a link relationship between an Azure AD user and the related user in Tango Analytics needs to be established.</span><span class="sxs-lookup"><span data-stu-id="cc1af-140">In other words, a link relationship between an Azure AD user and the related user in Tango Analytics needs to be established.</span></span>

<span data-ttu-id="cc1af-141">In Tango Analytics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="cc1af-141">In Tango Analytics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cc1af-142">To configure and test Azure AD single sign-on with Tango Analytics, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="cc1af-142">To configure and test Azure AD single sign-on with Tango Analytics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cc1af-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="cc1af-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="cc1af-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc1af-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="cc1af-145">**[Creating a Tango Analytics test user](#creating-a-tango-analytics-test-user)** - to have a counterpart of Britta Simon in Tango Analytics that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="cc1af-145">**[Creating a Tango Analytics test user](#creating-a-tango-analytics-test-user)** - to have a counterpart of Britta Simon in Tango Analytics that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="cc1af-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cc1af-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="cc1af-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="cc1af-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cc1af-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cc1af-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cc1af-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tango Analytics application.</span><span class="sxs-lookup"><span data-stu-id="cc1af-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tango Analytics application.</span></span>

<span data-ttu-id="cc1af-150">**To configure Azure AD single sign-on with Tango Analytics, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cc1af-150">**To configure Azure AD single sign-on with Tango Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="cc1af-151">In the Azure portal, on the **Tango Analytics** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="cc1af-151">In the Azure portal, on the **Tango Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="cc1af-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cc1af-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/tangoanalytics-tutorial/tutorial_tangoanalytics_samlbase.png)

1. <span data-ttu-id="cc1af-155">On the **Tango Analytics Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cc1af-155">On the **Tango Analytics Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/tangoanalytics-tutorial/tutorial_tangoanalytics_url.png)

    <span data-ttu-id="cc1af-157">a.</span><span class="sxs-lookup"><span data-stu-id="cc1af-157">a.</span></span> <span data-ttu-id="cc1af-158">In the **Identifier** textbox, type the value `TACORE_SSO`</span><span class="sxs-lookup"><span data-stu-id="cc1af-158">In the **Identifier** textbox, type the value `TACORE_SSO`</span></span>

    <span data-ttu-id="cc1af-159">b.</span><span class="sxs-lookup"><span data-stu-id="cc1af-159">b.</span></span> <span data-ttu-id="cc1af-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://mts.tangoanalytics.com/saml2/sp/acs/post`</span><span class="sxs-lookup"><span data-stu-id="cc1af-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://mts.tangoanalytics.com/saml2/sp/acs/post`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cc1af-161">The Reply URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="cc1af-161">The Reply URL value is not real.</span></span> <span data-ttu-id="cc1af-162">Update this with the actual Reply URL.</span><span class="sxs-lookup"><span data-stu-id="cc1af-162">Update this with the actual Reply URL.</span></span> <span data-ttu-id="cc1af-163">Contact [Tango Analytics support team](mailto:support@tangoanalytics.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="cc1af-163">Contact [Tango Analytics support team](mailto:support@tangoanalytics.com) to get this value.</span></span>

1. <span data-ttu-id="cc1af-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="cc1af-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/tangoanalytics-tutorial/tutorial_tangoanalytics_certificate.png) 

1. <span data-ttu-id="cc1af-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="cc1af-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/tangoanalytics-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="cc1af-168">To configure single sign-on on **Tango Analytics** side, you need to send the downloaded **Metadata XML** to [Tango Analytics support team](mailto:support@tangoanalytics.com).</span><span class="sxs-lookup"><span data-stu-id="cc1af-168">To configure single sign-on on **Tango Analytics** side, you need to send the downloaded **Metadata XML** to [Tango Analytics support team](mailto:support@tangoanalytics.com).</span></span> <span data-ttu-id="cc1af-169">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="cc1af-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="cc1af-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="cc1af-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cc1af-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="cc1af-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cc1af-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cc1af-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cc1af-173">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cc1af-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="cc1af-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc1af-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="cc1af-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cc1af-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cc1af-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="cc1af-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/tangoanalytics-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="cc1af-179">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="cc1af-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/tangoanalytics-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="cc1af-181">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="cc1af-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/tangoanalytics-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="cc1af-183">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cc1af-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/tangoanalytics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cc1af-185">a.</span><span class="sxs-lookup"><span data-stu-id="cc1af-185">a.</span></span> <span data-ttu-id="cc1af-186">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc1af-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc1af-187">b.</span><span class="sxs-lookup"><span data-stu-id="cc1af-187">b.</span></span> <span data-ttu-id="cc1af-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cc1af-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cc1af-189">c.</span><span class="sxs-lookup"><span data-stu-id="cc1af-189">c.</span></span> <span data-ttu-id="cc1af-190">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="cc1af-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cc1af-191">d.</span><span class="sxs-lookup"><span data-stu-id="cc1af-191">d.</span></span> <span data-ttu-id="cc1af-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="cc1af-192">Click **Create**.</span></span>
 
### <a name="creating-a-tango-analytics-test-user"></a><span data-ttu-id="cc1af-193">Creating a Tango Analytics test user</span><span class="sxs-lookup"><span data-stu-id="cc1af-193">Creating a Tango Analytics test user</span></span>

<span data-ttu-id="cc1af-194">In this section, you create a user called Britta Simon in Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="cc1af-194">In this section, you create a user called Britta Simon in Tango Analytics.</span></span> <span data-ttu-id="cc1af-195">Work with [Tango Analytics support team](mailto:support@tangoanalytics.com) to add the users in the Tango Analytics platform.</span><span class="sxs-lookup"><span data-stu-id="cc1af-195">Work with [Tango Analytics support team](mailto:support@tangoanalytics.com) to add the users in the Tango Analytics platform.</span></span> <span data-ttu-id="cc1af-196">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cc1af-196">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cc1af-197">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cc1af-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cc1af-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tango Analytics.</span><span class="sxs-lookup"><span data-stu-id="cc1af-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tango Analytics.</span></span>

![Assign User][200] 

<span data-ttu-id="cc1af-200">**To assign Britta Simon to Tango Analytics, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cc1af-200">**To assign Britta Simon to Tango Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="cc1af-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cc1af-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="cc1af-203">In the applications list, select **Tango Analytics**.</span><span class="sxs-lookup"><span data-stu-id="cc1af-203">In the applications list, select **Tango Analytics**.</span></span>

    ![Configure Single Sign-On](./media/tangoanalytics-tutorial/tutorial_tangoanalytics_app.png) 

1. <span data-ttu-id="cc1af-205">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="cc1af-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="cc1af-207">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="cc1af-207">Click **Add** button.</span></span> <span data-ttu-id="cc1af-208">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="cc1af-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="cc1af-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="cc1af-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="cc1af-211">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="cc1af-211">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="cc1af-212">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="cc1af-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cc1af-213">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="cc1af-213">Testing single sign-on</span></span>

<span data-ttu-id="cc1af-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="cc1af-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cc1af-215">When you click the Tango Analytics tile in the Access Panel, you should get automatically signed-on to your Tango Analytics application.</span><span class="sxs-lookup"><span data-stu-id="cc1af-215">When you click the Tango Analytics tile in the Access Panel, you should get automatically signed-on to your Tango Analytics application.</span></span>
<span data-ttu-id="cc1af-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cc1af-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cc1af-217">Additional resources</span><span class="sxs-lookup"><span data-stu-id="cc1af-217">Additional resources</span></span>

* [<span data-ttu-id="cc1af-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc1af-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="cc1af-219">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cc1af-219">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/tangoanalytics-tutorial/tutorial_general_01.png
[2]: ./media/tangoanalytics-tutorial/tutorial_general_02.png
[3]: ./media/tangoanalytics-tutorial/tutorial_general_03.png
[4]: ./media/tangoanalytics-tutorial/tutorial_general_04.png

[100]: ./media/tangoanalytics-tutorial/tutorial_general_100.png

[200]: ./media/tangoanalytics-tutorial/tutorial_general_200.png
[201]: ./media/tangoanalytics-tutorial/tutorial_general_201.png
[202]: ./media/tangoanalytics-tutorial/tutorial_general_202.png
[203]: ./media/tangoanalytics-tutorial/tutorial_general_203.png

