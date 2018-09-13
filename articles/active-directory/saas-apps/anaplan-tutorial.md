---
title: 'Tutorial: Azure Active Directory integration with Anaplan | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Anaplan.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 4a9c2914-6c8c-4a88-93e3-3753afb40e6b
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jeedes
ms.openlocfilehash: 4936e8d3c48486247677cf072513b7e450f1bf17
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867955"
---
# <a name="tutorial-azure-active-directory-integration-with-anaplan"></a><span data-ttu-id="289a4-103">Tutorial: Azure Active Directory integration with Anaplan</span><span class="sxs-lookup"><span data-stu-id="289a4-103">Tutorial: Azure Active Directory integration with Anaplan</span></span>

<span data-ttu-id="289a4-104">In this tutorial, you learn how to integrate Anaplan with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="289a4-104">In this tutorial, you learn how to integrate Anaplan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="289a4-105">Integrating Anaplan with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="289a4-105">Integrating Anaplan with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="289a4-106">You can control in Azure AD who has access to Anaplan</span><span class="sxs-lookup"><span data-stu-id="289a4-106">You can control in Azure AD who has access to Anaplan</span></span>
- <span data-ttu-id="289a4-107">You can enable your users to automatically get signed-on to Anaplan (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="289a4-107">You can enable your users to automatically get signed-on to Anaplan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="289a4-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="289a4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="289a4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="289a4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="289a4-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="289a4-110">Prerequisites</span></span>

<span data-ttu-id="289a4-111">To configure Azure AD integration with Anaplan, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="289a4-111">To configure Azure AD integration with Anaplan, you need the following items:</span></span>

- <span data-ttu-id="289a4-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="289a4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="289a4-113">An Anaplan single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="289a4-113">An Anaplan single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="289a4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="289a4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="289a4-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="289a4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="289a4-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="289a4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="289a4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="289a4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="289a4-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="289a4-118">Scenario description</span></span>
<span data-ttu-id="289a4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="289a4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="289a4-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="289a4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="289a4-121">Adding Anaplan from the gallery</span><span class="sxs-lookup"><span data-stu-id="289a4-121">Adding Anaplan from the gallery</span></span>
2. <span data-ttu-id="289a4-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="289a4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-anaplan-from-the-gallery"></a><span data-ttu-id="289a4-123">Adding Anaplan from the gallery</span><span class="sxs-lookup"><span data-stu-id="289a4-123">Adding Anaplan from the gallery</span></span>
<span data-ttu-id="289a4-124">To configure the integration of Anaplan into Azure AD, you need to add Anaplan from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="289a4-124">To configure the integration of Anaplan into Azure AD, you need to add Anaplan from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="289a4-125">**To add Anaplan from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="289a4-125">**To add Anaplan from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="289a4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="289a4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="289a4-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="289a4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="289a4-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="289a4-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="289a4-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="289a4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="289a4-133">In the search box, type **Anaplan**.</span><span class="sxs-lookup"><span data-stu-id="289a4-133">In the search box, type **Anaplan**.</span></span>

    ![Creating an Azure AD test user](./media/anaplan-tutorial/tutorial_anaplan_search.png)

5. <span data-ttu-id="289a4-135">In the results panel, select **Anaplan**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="289a4-135">In the results panel, select **Anaplan**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/anaplan-tutorial/tutorial_anaplan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="289a4-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="289a4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="289a4-138">In this section, you configure and test Azure AD single sign-on with Anaplan based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="289a4-138">In this section, you configure and test Azure AD single sign-on with Anaplan based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="289a4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Anaplan is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="289a4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Anaplan is to a user in Azure AD.</span></span> <span data-ttu-id="289a4-140">In other words, a link relationship between an Azure AD user and the related user in Anaplan needs to be established.</span><span class="sxs-lookup"><span data-stu-id="289a4-140">In other words, a link relationship between an Azure AD user and the related user in Anaplan needs to be established.</span></span>

<span data-ttu-id="289a4-141">In Anaplan, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="289a4-141">In Anaplan, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="289a4-142">To configure and test Azure AD single sign-on with Anaplan, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="289a4-142">To configure and test Azure AD single sign-on with Anaplan, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="289a4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="289a4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="289a4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="289a4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="289a4-145">**[Creating an Anaplan test user](#creating-an-anaplan-test-user)** - to have a counterpart of Britta Simon in Anaplan that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="289a4-145">**[Creating an Anaplan test user](#creating-an-anaplan-test-user)** - to have a counterpart of Britta Simon in Anaplan that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="289a4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="289a4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="289a4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="289a4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="289a4-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="289a4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="289a4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Anaplan application.</span><span class="sxs-lookup"><span data-stu-id="289a4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Anaplan application.</span></span>

<span data-ttu-id="289a4-150">**To configure Azure AD single sign-on with Anaplan, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="289a4-150">**To configure Azure AD single sign-on with Anaplan, perform the following steps:**</span></span>

1. <span data-ttu-id="289a4-151">In the Azure portal, on the **Anaplan** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="289a4-151">In the Azure portal, on the **Anaplan** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="289a4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="289a4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/anaplan-tutorial/tutorial_anaplan_samlbase.png)

3. <span data-ttu-id="289a4-155">On the **Anaplan Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="289a4-155">On the **Anaplan Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/anaplan-tutorial/tutorial_anaplan_url.png)

    <span data-ttu-id="289a4-157">a.</span><span class="sxs-lookup"><span data-stu-id="289a4-157">a.</span></span> <span data-ttu-id="289a4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sdp.anaplan.com/frontdoor/saml/<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="289a4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sdp.anaplan.com/frontdoor/saml/<tenant name>`</span></span>

    <span data-ttu-id="289a4-159">b.</span><span class="sxs-lookup"><span data-stu-id="289a4-159">b.</span></span> <span data-ttu-id="289a4-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.anaplan.com`</span><span class="sxs-lookup"><span data-stu-id="289a4-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.anaplan.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="289a4-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="289a4-161">These values are not real.</span></span> <span data-ttu-id="289a4-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="289a4-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="289a4-163">Contact [Anaplan Client support team](mailto:support@anaplan.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="289a4-163">Contact [Anaplan Client support team](mailto:support@anaplan.com) to get these values.</span></span> 
 
4. <span data-ttu-id="289a4-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="289a4-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/anaplan-tutorial/tutorial_anaplan_certificate.png) 

5. <span data-ttu-id="289a4-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="289a4-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/anaplan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="289a4-168">On the **Anaplan Configuration** section, click **Configure Anaplan** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="289a4-168">On the **Anaplan Configuration** section, click **Configure Anaplan** to open **Configure sign-on** window.</span></span> <span data-ttu-id="289a4-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="289a4-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/anaplan-tutorial/tutorial_anaplan_configure.png) 

7. <span data-ttu-id="289a4-171">To configure single sign-on on **Anaplan** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL**   to [Anaplan support team](mailto:support@anaplan.com).</span><span class="sxs-lookup"><span data-stu-id="289a4-171">To configure single sign-on on **Anaplan** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL**   to [Anaplan support team](mailto:support@anaplan.com).</span></span> <span data-ttu-id="289a4-172">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="289a4-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="289a4-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="289a4-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="289a4-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="289a4-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="289a4-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="289a4-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="289a4-176">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="289a4-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="289a4-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="289a4-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="289a4-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="289a4-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="289a4-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="289a4-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/anaplan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="289a4-182">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="289a4-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/anaplan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="289a4-184">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="289a4-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/anaplan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="289a4-186">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="289a4-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/anaplan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="289a4-188">a.</span><span class="sxs-lookup"><span data-stu-id="289a4-188">a.</span></span> <span data-ttu-id="289a4-189">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="289a4-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="289a4-190">b.</span><span class="sxs-lookup"><span data-stu-id="289a4-190">b.</span></span> <span data-ttu-id="289a4-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="289a4-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="289a4-192">c.</span><span class="sxs-lookup"><span data-stu-id="289a4-192">c.</span></span> <span data-ttu-id="289a4-193">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="289a4-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="289a4-194">d.</span><span class="sxs-lookup"><span data-stu-id="289a4-194">d.</span></span> <span data-ttu-id="289a4-195">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="289a4-195">Click **Create**.</span></span>
 
### <a name="creating-an-anaplan-test-user"></a><span data-ttu-id="289a4-196">Creating an Anaplan test user</span><span class="sxs-lookup"><span data-stu-id="289a4-196">Creating an Anaplan test user</span></span>

<span data-ttu-id="289a4-197">In this section, you create a user called Britta Simon in Anaplan.</span><span class="sxs-lookup"><span data-stu-id="289a4-197">In this section, you create a user called Britta Simon in Anaplan.</span></span> <span data-ttu-id="289a4-198">Please work with [Anaplan support team](mailto:support@anaplan.com) to add the users in the Anaplan platform.</span><span class="sxs-lookup"><span data-stu-id="289a4-198">Please work with [Anaplan support team](mailto:support@anaplan.com) to add the users in the Anaplan platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="289a4-199">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="289a4-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="289a4-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Anaplan.</span><span class="sxs-lookup"><span data-stu-id="289a4-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Anaplan.</span></span>

![Assign User][200] 

<span data-ttu-id="289a4-202">**To assign Britta Simon to Anaplan, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="289a4-202">**To assign Britta Simon to Anaplan, perform the following steps:**</span></span>

1. <span data-ttu-id="289a4-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="289a4-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="289a4-205">In the applications list, select **Anaplan**.</span><span class="sxs-lookup"><span data-stu-id="289a4-205">In the applications list, select **Anaplan**.</span></span>

    ![Configure Single Sign-On](./media/anaplan-tutorial/tutorial_anaplan_app.png) 

3. <span data-ttu-id="289a4-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="289a4-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="289a4-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="289a4-209">Click **Add** button.</span></span> <span data-ttu-id="289a4-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="289a4-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="289a4-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="289a4-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="289a4-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="289a4-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="289a4-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="289a4-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="289a4-215">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="289a4-215">Testing single sign-on</span></span>

<span data-ttu-id="289a4-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="289a4-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="289a4-217">When you click the Anaplan tile in the Access Panel, you should get automatically signed-on to your Anaplan application.</span><span class="sxs-lookup"><span data-stu-id="289a4-217">When you click the Anaplan tile in the Access Panel, you should get automatically signed-on to your Anaplan application.</span></span>

<span data-ttu-id="289a4-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="289a4-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="289a4-219">Additional resources</span><span class="sxs-lookup"><span data-stu-id="289a4-219">Additional resources</span></span>

* [<span data-ttu-id="289a4-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="289a4-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="289a4-221">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="289a4-221">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)


<!--Image references-->

[1]: ./media/anaplan-tutorial/tutorial_general_01.png
[2]: ./media/anaplan-tutorial/tutorial_general_02.png
[3]: ./media/anaplan-tutorial/tutorial_general_03.png
[4]: ./media/anaplan-tutorial/tutorial_general_04.png

[100]: ./media/anaplan-tutorial/tutorial_general_100.png

[200]: ./media/anaplan-tutorial/tutorial_general_200.png
[201]: ./media/anaplan-tutorial/tutorial_general_201.png
[202]: ./media/anaplan-tutorial/tutorial_general_202.png
[203]: ./media/anaplan-tutorial/tutorial_general_203.png

