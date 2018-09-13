---
title: 'Tutorial: Azure Active Directory integration with Pacific Timesheet | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Pacific Timesheet.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: e546e8ba-821a-4942-9545-c84b0670beab
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 051e39d0e7a58c79eb00bc3dfb73eaf5389617c8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857191"
---
# <a name="tutorial-azure-active-directory-integration-with-pacific-timesheet"></a><span data-ttu-id="727e2-103">Tutorial: Azure Active Directory integration with Pacific Timesheet</span><span class="sxs-lookup"><span data-stu-id="727e2-103">Tutorial: Azure Active Directory integration with Pacific Timesheet</span></span>

<span data-ttu-id="727e2-104">In this tutorial, you learn how to integrate Pacific Timesheet with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="727e2-104">In this tutorial, you learn how to integrate Pacific Timesheet with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="727e2-105">Integrating Pacific Timesheet with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="727e2-105">Integrating Pacific Timesheet with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="727e2-106">You can control in Azure AD who has access to Pacific Timesheet</span><span class="sxs-lookup"><span data-stu-id="727e2-106">You can control in Azure AD who has access to Pacific Timesheet</span></span>
- <span data-ttu-id="727e2-107">You can enable your users to automatically get signed-on to Pacific Timesheet (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="727e2-107">You can enable your users to automatically get signed-on to Pacific Timesheet (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="727e2-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="727e2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="727e2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="727e2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="727e2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="727e2-110">Prerequisites</span></span>

<span data-ttu-id="727e2-111">To configure Azure AD integration with Pacific Timesheet, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="727e2-111">To configure Azure AD integration with Pacific Timesheet, you need the following items:</span></span>

- <span data-ttu-id="727e2-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="727e2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="727e2-113">A Pacific Timesheet single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="727e2-113">A Pacific Timesheet single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="727e2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="727e2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="727e2-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="727e2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="727e2-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="727e2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="727e2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="727e2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="727e2-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="727e2-118">Scenario description</span></span>
<span data-ttu-id="727e2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="727e2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="727e2-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="727e2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="727e2-121">Adding Pacific Timesheet from the gallery</span><span class="sxs-lookup"><span data-stu-id="727e2-121">Adding Pacific Timesheet from the gallery</span></span>
1. <span data-ttu-id="727e2-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="727e2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pacific-timesheet-from-the-gallery"></a><span data-ttu-id="727e2-123">Adding Pacific Timesheet from the gallery</span><span class="sxs-lookup"><span data-stu-id="727e2-123">Adding Pacific Timesheet from the gallery</span></span>
<span data-ttu-id="727e2-124">To configure the integration of Pacific Timesheet into Azure AD, you need to add Pacific Timesheet from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="727e2-124">To configure the integration of Pacific Timesheet into Azure AD, you need to add Pacific Timesheet from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="727e2-125">**To add Pacific Timesheet from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="727e2-125">**To add Pacific Timesheet from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="727e2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="727e2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="727e2-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="727e2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="727e2-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="727e2-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="727e2-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="727e2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="727e2-133">In the search box, type **Pacific Timesheet**.</span><span class="sxs-lookup"><span data-stu-id="727e2-133">In the search box, type **Pacific Timesheet**.</span></span>

    ![Creating an Azure AD test user](./media/pacific-timesheet-tutorial/tutorial_pacifictimesheet_search.png)

1. <span data-ttu-id="727e2-135">In the results panel, select **Pacific Timesheet**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="727e2-135">In the results panel, select **Pacific Timesheet**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/pacific-timesheet-tutorial/tutorial_pacifictimesheet_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="727e2-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="727e2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="727e2-138">In this section, you configure and test Azure AD single sign-on with Pacific Timesheet based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="727e2-138">In this section, you configure and test Azure AD single sign-on with Pacific Timesheet based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="727e2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pacific Timesheet is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="727e2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pacific Timesheet is to a user in Azure AD.</span></span> <span data-ttu-id="727e2-140">In other words, a link relationship between an Azure AD user and the related user in Pacific Timesheet needs to be established.</span><span class="sxs-lookup"><span data-stu-id="727e2-140">In other words, a link relationship between an Azure AD user and the related user in Pacific Timesheet needs to be established.</span></span>

<span data-ttu-id="727e2-141">In Pacific Timesheet, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="727e2-141">In Pacific Timesheet, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="727e2-142">To configure and test Azure AD single sign-on with Pacific Timesheet, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="727e2-142">To configure and test Azure AD single sign-on with Pacific Timesheet, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="727e2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="727e2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="727e2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="727e2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="727e2-145">**[Creating a Pacific Timesheet test user](#creating-a-pacific-timesheet-test-user)** - to have a counterpart of Britta Simon in Pacific Timesheet that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="727e2-145">**[Creating a Pacific Timesheet test user](#creating-a-pacific-timesheet-test-user)** - to have a counterpart of Britta Simon in Pacific Timesheet that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="727e2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="727e2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="727e2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="727e2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="727e2-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="727e2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="727e2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pacific Timesheet application.</span><span class="sxs-lookup"><span data-stu-id="727e2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pacific Timesheet application.</span></span>

<span data-ttu-id="727e2-150">**To configure Azure AD single sign-on with Pacific Timesheet, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="727e2-150">**To configure Azure AD single sign-on with Pacific Timesheet, perform the following steps:**</span></span>

1. <span data-ttu-id="727e2-151">In the Azure portal, on the **Pacific Timesheet** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="727e2-151">In the Azure portal, on the **Pacific Timesheet** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="727e2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="727e2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/pacific-timesheet-tutorial/tutorial_pacifictimesheet_samlbase.png)

1. <span data-ttu-id="727e2-155">On the **Pacific Timesheet Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="727e2-155">On the **Pacific Timesheet Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/pacific-timesheet-tutorial/tutorial_pacifictimesheet_url.png)

    <span data-ttu-id="727e2-157">a.</span><span class="sxs-lookup"><span data-stu-id="727e2-157">a.</span></span> <span data-ttu-id="727e2-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span><span class="sxs-lookup"><span data-stu-id="727e2-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span></span>

    <span data-ttu-id="727e2-159">b.</span><span class="sxs-lookup"><span data-stu-id="727e2-159">b.</span></span> <span data-ttu-id="727e2-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span><span class="sxs-lookup"><span data-stu-id="727e2-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="727e2-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="727e2-161">These values are not real.</span></span> <span data-ttu-id="727e2-162">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="727e2-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="727e2-163">Contact [Pacific Timesheet support team](http://www.pacifictimesheet.com/support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="727e2-163">Contact [Pacific Timesheet support team](http://www.pacifictimesheet.com/support) to get these values.</span></span>
 
1. <span data-ttu-id="727e2-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="727e2-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/pacific-timesheet-tutorial/tutorial_pacifictimesheet_certificate.png) 

1. <span data-ttu-id="727e2-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="727e2-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/pacific-timesheet-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="727e2-168">On the **Pacific Timesheet Configuration** section, click **Configure Pacific Timesheet** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="727e2-168">On the **Pacific Timesheet Configuration** section, click **Configure Pacific Timesheet** to open **Configure sign-on** window.</span></span> <span data-ttu-id="727e2-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="727e2-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/pacific-timesheet-tutorial/tutorial_pacifictimesheet_configure.png) 

1. <span data-ttu-id="727e2-171">To configure single sign-on on **Pacific Timesheet** side, you need to send the downloaded **Certificate (Base64)**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** to [Pacific Timesheet support team](http://www.pacifictimesheet.com/support).</span><span class="sxs-lookup"><span data-stu-id="727e2-171">To configure single sign-on on **Pacific Timesheet** side, you need to send the downloaded **Certificate (Base64)**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** to [Pacific Timesheet support team](http://www.pacifictimesheet.com/support).</span></span> <span data-ttu-id="727e2-172">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="727e2-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="727e2-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="727e2-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="727e2-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="727e2-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="727e2-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="727e2-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="727e2-176">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="727e2-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="727e2-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="727e2-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="727e2-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="727e2-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="727e2-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="727e2-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/pacific-timesheet-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="727e2-182">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="727e2-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/pacific-timesheet-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="727e2-184">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="727e2-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/pacific-timesheet-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="727e2-186">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="727e2-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/pacific-timesheet-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="727e2-188">a.</span><span class="sxs-lookup"><span data-stu-id="727e2-188">a.</span></span> <span data-ttu-id="727e2-189">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="727e2-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="727e2-190">b.</span><span class="sxs-lookup"><span data-stu-id="727e2-190">b.</span></span> <span data-ttu-id="727e2-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="727e2-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="727e2-192">c.</span><span class="sxs-lookup"><span data-stu-id="727e2-192">c.</span></span> <span data-ttu-id="727e2-193">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="727e2-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="727e2-194">d.</span><span class="sxs-lookup"><span data-stu-id="727e2-194">d.</span></span> <span data-ttu-id="727e2-195">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="727e2-195">Click **Create**.</span></span>
 
### <a name="creating-a-pacific-timesheet-test-user"></a><span data-ttu-id="727e2-196">Creating a Pacific Timesheet test user</span><span class="sxs-lookup"><span data-stu-id="727e2-196">Creating a Pacific Timesheet test user</span></span>

<span data-ttu-id="727e2-197">In this section, you create a user called Britta Simon in Pacific Timesheet.</span><span class="sxs-lookup"><span data-stu-id="727e2-197">In this section, you create a user called Britta Simon in Pacific Timesheet.</span></span> <span data-ttu-id="727e2-198">Work with [Pacific Timesheet support team](http://www.pacifictimesheet.com/support) to create a user in the application.</span><span class="sxs-lookup"><span data-stu-id="727e2-198">Work with [Pacific Timesheet support team](http://www.pacifictimesheet.com/support) to create a user in the application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="727e2-199">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="727e2-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="727e2-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pacific Timesheet.</span><span class="sxs-lookup"><span data-stu-id="727e2-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pacific Timesheet.</span></span>

![Assign User][200] 

<span data-ttu-id="727e2-202">**To assign Britta Simon to Pacific Timesheet, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="727e2-202">**To assign Britta Simon to Pacific Timesheet, perform the following steps:**</span></span>

1. <span data-ttu-id="727e2-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="727e2-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="727e2-205">In the applications list, select **Pacific Timesheet**.</span><span class="sxs-lookup"><span data-stu-id="727e2-205">In the applications list, select **Pacific Timesheet**.</span></span>

    ![Configure Single Sign-On](./media/pacific-timesheet-tutorial/tutorial_pacifictimesheet_app.png) 

1. <span data-ttu-id="727e2-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="727e2-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="727e2-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="727e2-209">Click **Add** button.</span></span> <span data-ttu-id="727e2-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="727e2-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="727e2-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="727e2-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="727e2-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="727e2-213">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="727e2-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="727e2-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="727e2-215">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="727e2-215">Testing single sign-on</span></span>

<span data-ttu-id="727e2-216">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="727e2-216">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="727e2-217">When you click the Pacific Timesheet tile in the Access Panel, you should get automatically signed-on to your Pacific Timesheet application.</span><span class="sxs-lookup"><span data-stu-id="727e2-217">When you click the Pacific Timesheet tile in the Access Panel, you should get automatically signed-on to your Pacific Timesheet application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="727e2-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="727e2-218">Additional resources</span></span>

* [<span data-ttu-id="727e2-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="727e2-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="727e2-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="727e2-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/pacific-timesheet-tutorial/tutorial_general_01.png
[2]: ./media/pacific-timesheet-tutorial/tutorial_general_02.png
[3]: ./media/pacific-timesheet-tutorial/tutorial_general_03.png
[4]: ./media/pacific-timesheet-tutorial/tutorial_general_04.png

[100]: ./media/pacific-timesheet-tutorial/tutorial_general_100.png

[200]: ./media/pacific-timesheet-tutorial/tutorial_general_200.png
[201]: ./media/pacific-timesheet-tutorial/tutorial_general_201.png
[202]: ./media/pacific-timesheet-tutorial/tutorial_general_202.png
[203]: ./media/pacific-timesheet-tutorial/tutorial_general_203.png

