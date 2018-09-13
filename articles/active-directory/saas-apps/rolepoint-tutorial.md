---
title: 'Tutorial: Azure Active Directory integration with RolePoint | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and RolePoint.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 68d37f40-15da-45f5-a9e1-d53f78e786d1
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: jeedes
ms.openlocfilehash: 1cefb855e089f540946dbd11005f384c33027df7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870371"
---
# <a name="tutorial-azure-active-directory-integration-with-rolepoint"></a><span data-ttu-id="17dff-103">Tutorial: Azure Active Directory integration with RolePoint</span><span class="sxs-lookup"><span data-stu-id="17dff-103">Tutorial: Azure Active Directory integration with RolePoint</span></span>

<span data-ttu-id="17dff-104">In this tutorial, you learn how to integrate RolePoint with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="17dff-104">In this tutorial, you learn how to integrate RolePoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17dff-105">Integrating RolePoint with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="17dff-105">Integrating RolePoint with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="17dff-106">You can control in Azure AD who has access to RolePoint</span><span class="sxs-lookup"><span data-stu-id="17dff-106">You can control in Azure AD who has access to RolePoint</span></span>
- <span data-ttu-id="17dff-107">You can enable your users to automatically get signed-on to RolePoint (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="17dff-107">You can enable your users to automatically get signed-on to RolePoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="17dff-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="17dff-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="17dff-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="17dff-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17dff-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="17dff-110">Prerequisites</span></span>

<span data-ttu-id="17dff-111">To configure Azure AD integration with RolePoint, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="17dff-111">To configure Azure AD integration with RolePoint, you need the following items:</span></span>

- <span data-ttu-id="17dff-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="17dff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17dff-113">A RolePoint single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="17dff-113">A RolePoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17dff-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="17dff-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17dff-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="17dff-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17dff-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="17dff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="17dff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17dff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17dff-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="17dff-118">Scenario description</span></span>
<span data-ttu-id="17dff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="17dff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17dff-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="17dff-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17dff-121">Adding RolePoint from the gallery</span><span class="sxs-lookup"><span data-stu-id="17dff-121">Adding RolePoint from the gallery</span></span>
1. <span data-ttu-id="17dff-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="17dff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rolepoint-from-the-gallery"></a><span data-ttu-id="17dff-123">Adding RolePoint from the gallery</span><span class="sxs-lookup"><span data-stu-id="17dff-123">Adding RolePoint from the gallery</span></span>
<span data-ttu-id="17dff-124">To configure the integration of RolePoint into Azure AD, you need to add RolePoint from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="17dff-124">To configure the integration of RolePoint into Azure AD, you need to add RolePoint from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="17dff-125">**To add RolePoint from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="17dff-125">**To add RolePoint from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="17dff-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="17dff-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="17dff-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="17dff-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="17dff-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="17dff-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="17dff-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="17dff-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="17dff-133">In the search box, type **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="17dff-133">In the search box, type **RolePoint**.</span></span>

    ![Creating an Azure AD test user](./media/rolepoint-tutorial/tutorial_rolepoint_search.png)

1. <span data-ttu-id="17dff-135">In the results panel, select **RolePoint**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="17dff-135">In the results panel, select **RolePoint**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/rolepoint-tutorial/tutorial_rolepoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="17dff-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="17dff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="17dff-138">In this section, you configure and test Azure AD single sign-on with RolePoint based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="17dff-138">In this section, you configure and test Azure AD single sign-on with RolePoint based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="17dff-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RolePoint is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17dff-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RolePoint is to a user in Azure AD.</span></span> <span data-ttu-id="17dff-140">In other words, a link relationship between an Azure AD user and the related user in RolePoint needs to be established.</span><span class="sxs-lookup"><span data-stu-id="17dff-140">In other words, a link relationship between an Azure AD user and the related user in RolePoint needs to be established.</span></span>

<span data-ttu-id="17dff-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in RolePoint.</span><span class="sxs-lookup"><span data-stu-id="17dff-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in RolePoint.</span></span>

<span data-ttu-id="17dff-142">To configure and test Azure AD single sign-on with RolePoint, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="17dff-142">To configure and test Azure AD single sign-on with RolePoint, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="17dff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="17dff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="17dff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17dff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="17dff-145">**[Creating a RolePoint test user](#creating-a-rolepoint-test-user)** - to have a counterpart of Britta Simon in RolePoint that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="17dff-145">**[Creating a RolePoint test user](#creating-a-rolepoint-test-user)** - to have a counterpart of Britta Simon in RolePoint that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="17dff-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="17dff-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="17dff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="17dff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="17dff-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="17dff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="17dff-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RolePoint application.</span><span class="sxs-lookup"><span data-stu-id="17dff-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RolePoint application.</span></span>

<span data-ttu-id="17dff-150">**To configure Azure AD single sign-on with RolePoint, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="17dff-150">**To configure Azure AD single sign-on with RolePoint, perform the following steps:**</span></span>

1. <span data-ttu-id="17dff-151">In the Azure portal, on the **RolePoint** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="17dff-151">In the Azure portal, on the **RolePoint** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="17dff-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="17dff-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/rolepoint-tutorial/tutorial_rolepoint_samlbase.png)

1. <span data-ttu-id="17dff-155">On the **RolePoint Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="17dff-155">On the **RolePoint Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/rolepoint-tutorial/tutorial_rolepoint_url.png)

    <span data-ttu-id="17dff-157">a.</span><span class="sxs-lookup"><span data-stu-id="17dff-157">a.</span></span> <span data-ttu-id="17dff-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.rolepoint.com/login`</span><span class="sxs-lookup"><span data-stu-id="17dff-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.rolepoint.com/login`</span></span>
    
    <span data-ttu-id="17dff-159">b.</span><span class="sxs-lookup"><span data-stu-id="17dff-159">b.</span></span> <span data-ttu-id="17dff-160">In the **Identifier** textbox, type a URL using the following pattern: `https://app.rolepoint.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="17dff-160">In the **Identifier** textbox, type a URL using the following pattern: `https://app.rolepoint.com/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="17dff-161">These values are not the real.</span><span class="sxs-lookup"><span data-stu-id="17dff-161">These values are not the real.</span></span> <span data-ttu-id="17dff-162">Update these values with the actual Sign-on URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="17dff-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="17dff-163">Here we suggest you to use the unique value of string in the Identifier.Contact [RolePoint support team](mailto:info@rolepoint.com) to get the value.</span><span class="sxs-lookup"><span data-stu-id="17dff-163">Here we suggest you to use the unique value of string in the Identifier.Contact [RolePoint support team](mailto:info@rolepoint.com) to get the value.</span></span> 
 
1. <span data-ttu-id="17dff-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="17dff-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/rolepoint-tutorial/tutorial_rolepoint_certificate.png) 

1. <span data-ttu-id="17dff-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="17dff-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/rolepoint-tutorial/tutorial_general_400.png)


1. <span data-ttu-id="17dff-168">To configure single sign-on on **RolePoint** side, you need to send the downloaded **Metadata XML** to [RolePoint support team](mailto:info@rolepoint.com).</span><span class="sxs-lookup"><span data-stu-id="17dff-168">To configure single sign-on on **RolePoint** side, you need to send the downloaded **Metadata XML** to [RolePoint support team](mailto:info@rolepoint.com).</span></span>

> [!TIP]
> <span data-ttu-id="17dff-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="17dff-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="17dff-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="17dff-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="17dff-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="17dff-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="17dff-172">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="17dff-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="17dff-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17dff-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="17dff-175">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="17dff-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="17dff-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="17dff-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/rolepoint-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="17dff-178">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="17dff-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/rolepoint-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="17dff-180">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="17dff-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/rolepoint-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="17dff-182">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="17dff-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/rolepoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="17dff-184">a.</span><span class="sxs-lookup"><span data-stu-id="17dff-184">a.</span></span> <span data-ttu-id="17dff-185">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="17dff-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="17dff-186">b.</span><span class="sxs-lookup"><span data-stu-id="17dff-186">b.</span></span> <span data-ttu-id="17dff-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="17dff-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="17dff-188">c.</span><span class="sxs-lookup"><span data-stu-id="17dff-188">c.</span></span> <span data-ttu-id="17dff-189">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="17dff-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="17dff-190">d.</span><span class="sxs-lookup"><span data-stu-id="17dff-190">d.</span></span> <span data-ttu-id="17dff-191">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="17dff-191">Click **Create**.</span></span>
 
### <a name="creating-a-rolepoint-test-user"></a><span data-ttu-id="17dff-192">Creating a RolePoint test user</span><span class="sxs-lookup"><span data-stu-id="17dff-192">Creating a RolePoint test user</span></span>

<span data-ttu-id="17dff-193">In this section, you create a user called Britta Simon in RolePoint.</span><span class="sxs-lookup"><span data-stu-id="17dff-193">In this section, you create a user called Britta Simon in RolePoint.</span></span> <span data-ttu-id="17dff-194">Work with [RolePoint support team](mailto:info@rolepoint.com) to add the users in the RolePoint platform.</span><span class="sxs-lookup"><span data-stu-id="17dff-194">Work with [RolePoint support team](mailto:info@rolepoint.com) to add the users in the RolePoint platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="17dff-195">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="17dff-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="17dff-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RolePoint.</span><span class="sxs-lookup"><span data-stu-id="17dff-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RolePoint.</span></span>

![Assign User][200] 

<span data-ttu-id="17dff-198">**To assign Britta Simon to RolePoint, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="17dff-198">**To assign Britta Simon to RolePoint, perform the following steps:**</span></span>

1. <span data-ttu-id="17dff-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="17dff-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="17dff-201">In the applications list, select **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="17dff-201">In the applications list, select **RolePoint**.</span></span>

    ![Configure Single Sign-On](./media/rolepoint-tutorial/tutorial_rolepoint_app.png) 

1. <span data-ttu-id="17dff-203">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="17dff-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="17dff-205">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="17dff-205">Click **Add** button.</span></span> <span data-ttu-id="17dff-206">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="17dff-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="17dff-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="17dff-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="17dff-209">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="17dff-209">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="17dff-210">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="17dff-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="17dff-211">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="17dff-211">Testing single sign-on</span></span>

<span data-ttu-id="17dff-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="17dff-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="17dff-213">When you click the RolePoint tile in the Access Panel, you should get automatically signed-on to your RolePoint application.</span><span class="sxs-lookup"><span data-stu-id="17dff-213">When you click the RolePoint tile in the Access Panel, you should get automatically signed-on to your RolePoint application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="17dff-214">Additional resources</span><span class="sxs-lookup"><span data-stu-id="17dff-214">Additional resources</span></span>

* [<span data-ttu-id="17dff-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17dff-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="17dff-216">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="17dff-216">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/rolepoint-tutorial/tutorial_general_01.png
[2]: ./media/rolepoint-tutorial/tutorial_general_02.png
[3]: ./media/rolepoint-tutorial/tutorial_general_03.png
[4]: ./media/rolepoint-tutorial/tutorial_general_04.png

[100]: ./media/rolepoint-tutorial/tutorial_general_100.png

[200]: ./media/rolepoint-tutorial/tutorial_general_200.png
[201]: ./media/rolepoint-tutorial/tutorial_general_201.png
[202]: ./media/rolepoint-tutorial/tutorial_general_202.png
[203]: ./media/rolepoint-tutorial/tutorial_general_203.png

