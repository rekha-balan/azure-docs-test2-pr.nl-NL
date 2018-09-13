---
title: 'Tutorial: Azure Active Directory integration with Overdrive | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Overdrive .
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: e68cede7-1130-4813-bd55-22a9a6fc6bf5
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 3d4df5db47cb8007599ca2a09608b23f382e3fbb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869122"
---
# <a name="tutorial-azure-active-directory-integration-with-overdrive"></a><span data-ttu-id="a9011-103">Tutorial: Azure Active Directory integration with Overdrive</span><span class="sxs-lookup"><span data-stu-id="a9011-103">Tutorial: Azure Active Directory integration with Overdrive</span></span> 

<span data-ttu-id="a9011-104">In this tutorial, you learn how to integrate Overdrive with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a9011-104">In this tutorial, you learn how to integrate Overdrive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a9011-105">Integrating Overdrive with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a9011-105">Integrating Overdrive with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a9011-106">You can control in Azure AD who has access to Overdrive</span><span class="sxs-lookup"><span data-stu-id="a9011-106">You can control in Azure AD who has access to Overdrive</span></span> 
- <span data-ttu-id="a9011-107">You can enable your users to automatically get signed-on to Overdrive (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="a9011-107">You can enable your users to automatically get signed-on to Overdrive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a9011-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a9011-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a9011-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a9011-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9011-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a9011-110">Prerequisites</span></span>

<span data-ttu-id="a9011-111">To configure Azure AD integration with Overdrive, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a9011-111">To configure Azure AD integration with Overdrive, you need the following items:</span></span>

- <span data-ttu-id="a9011-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a9011-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a9011-113">An Overdrive single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a9011-113">An Overdrive single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a9011-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a9011-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a9011-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a9011-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a9011-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a9011-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a9011-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a9011-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a9011-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a9011-118">Scenario description</span></span>
<span data-ttu-id="a9011-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a9011-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a9011-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a9011-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a9011-121">Adding Overdrive from the gallery</span><span class="sxs-lookup"><span data-stu-id="a9011-121">Adding Overdrive from the gallery</span></span>
1. <span data-ttu-id="a9011-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a9011-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-overdrive-from-the-gallery"></a><span data-ttu-id="a9011-123">Adding Overdrive from the gallery</span><span class="sxs-lookup"><span data-stu-id="a9011-123">Adding Overdrive from the gallery</span></span>
<span data-ttu-id="a9011-124">To configure the integration of Overdrive into Azure AD, you need to add Overdrive from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a9011-124">To configure the integration of Overdrive into Azure AD, you need to add Overdrive from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a9011-125">**To add Overdrive from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9011-125">**To add Overdrive from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a9011-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a9011-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="a9011-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a9011-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a9011-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a9011-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="a9011-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a9011-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="a9011-133">In the search box, type **Overdrive**.</span><span class="sxs-lookup"><span data-stu-id="a9011-133">In the search box, type **Overdrive**.</span></span>

    ![Creating an Azure AD test user](./media/overdrive-books-tutorial/tutorial_overdrivebooks_search.png)

1. <span data-ttu-id="a9011-135">In the results panel, select **Overdrive**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a9011-135">In the results panel, select **Overdrive**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/overdrive-books-tutorial/tutorial_overdrivebooks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a9011-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a9011-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a9011-138">In this section, you configure and test Azure AD single sign-on with Overdrive based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a9011-138">In this section, you configure and test Azure AD single sign-on with Overdrive based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a9011-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Overdrive is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9011-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Overdrive is to a user in Azure AD.</span></span> <span data-ttu-id="a9011-140">In other words, a link relationship between an Azure AD user and the related user in Overdrive needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a9011-140">In other words, a link relationship between an Azure AD user and the related user in Overdrive needs to be established.</span></span>

<span data-ttu-id="a9011-141">In Overdrive, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="a9011-141">In Overdrive, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a9011-142">To configure and test Azure AD single sign-on with Overdrive, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a9011-142">To configure and test Azure AD single sign-on with Overdrive, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a9011-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a9011-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="a9011-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9011-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="a9011-145">**[Creating an Overdrive test user](#creating-an-overdrive-test-user)** - to have a counterpart of Britta Simon in Overdrive that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a9011-145">**[Creating an Overdrive test user](#creating-an-overdrive-test-user)** - to have a counterpart of Britta Simon in Overdrive that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="a9011-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a9011-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="a9011-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a9011-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a9011-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a9011-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a9011-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Overdrive  application.</span><span class="sxs-lookup"><span data-stu-id="a9011-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Overdrive  application.</span></span>

<span data-ttu-id="a9011-150">**To configure Azure AD single sign-on with Overdrive, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9011-150">**To configure Azure AD single sign-on with Overdrive, perform the following steps:**</span></span>

1. <span data-ttu-id="a9011-151">In the Azure portal, on the **Overdrive** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a9011-151">In the Azure portal, on the **Overdrive** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="a9011-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a9011-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/overdrive-books-tutorial/tutorial_overdrivebooks_samlbase.png)

1. <span data-ttu-id="a9011-155">On the **Overdrive Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a9011-155">On the **Overdrive Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/overdrive-books-tutorial/tutorial_overdrivebooks_url.png)

    <span data-ttu-id="a9011-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<subdomain>.libraryreserve.com`</span><span class="sxs-lookup"><span data-stu-id="a9011-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<subdomain>.libraryreserve.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a9011-158">The value is not real.</span><span class="sxs-lookup"><span data-stu-id="a9011-158">The value is not real.</span></span> <span data-ttu-id="a9011-159">Update the value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="a9011-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="a9011-160">Contact [Overdrive Client support team](https://help.overdrive.com/) to get the value.</span><span class="sxs-lookup"><span data-stu-id="a9011-160">Contact [Overdrive Client support team](https://help.overdrive.com/) to get the value.</span></span> 
 
1. <span data-ttu-id="a9011-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a9011-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/overdrive-books-tutorial/tutorial_overdrivebooks_certificate.png) 

1. <span data-ttu-id="a9011-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a9011-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/overdrive-books-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="a9011-165">To configure single sign-on on **Overdrive** side, you need to send the downloaded **Metadata XML** to [Overdrive support team](https://help.overdrive.com/).</span><span class="sxs-lookup"><span data-stu-id="a9011-165">To configure single sign-on on **Overdrive** side, you need to send the downloaded **Metadata XML** to [Overdrive support team](https://help.overdrive.com/).</span></span> <span data-ttu-id="a9011-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="a9011-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a9011-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="a9011-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a9011-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="a9011-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a9011-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a9011-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a9011-170">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a9011-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="a9011-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9011-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="a9011-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9011-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a9011-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a9011-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/overdrive-books-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="a9011-176">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a9011-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/overdrive-books-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="a9011-178">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="a9011-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/overdrive-books-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="a9011-180">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a9011-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/overdrive-books-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a9011-182">a.</span><span class="sxs-lookup"><span data-stu-id="a9011-182">a.</span></span> <span data-ttu-id="a9011-183">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a9011-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a9011-184">b.</span><span class="sxs-lookup"><span data-stu-id="a9011-184">b.</span></span> <span data-ttu-id="a9011-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a9011-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a9011-186">c.</span><span class="sxs-lookup"><span data-stu-id="a9011-186">c.</span></span> <span data-ttu-id="a9011-187">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="a9011-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a9011-188">d.</span><span class="sxs-lookup"><span data-stu-id="a9011-188">d.</span></span> <span data-ttu-id="a9011-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a9011-189">Click **Create**.</span></span>
 
### <a name="creating-an-overdrive-test-user"></a><span data-ttu-id="a9011-190">Creating an Overdrive test user</span><span class="sxs-lookup"><span data-stu-id="a9011-190">Creating an Overdrive test user</span></span>

<span data-ttu-id="a9011-191">There is no action item for you to configure user provisioning to OverDrive.</span><span class="sxs-lookup"><span data-stu-id="a9011-191">There is no action item for you to configure user provisioning to OverDrive.</span></span>  

<span data-ttu-id="a9011-192">When an assigned user tries to log in to OverDrive, an OverDrive account is automatically created if necessary.</span><span class="sxs-lookup"><span data-stu-id="a9011-192">When an assigned user tries to log in to OverDrive, an OverDrive account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="a9011-193">You can use any other OverDrive user account creation tools or APIs provided by OverDrive to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="a9011-193">You can use any other OverDrive user account creation tools or APIs provided by OverDrive to provision AAD user accounts.</span></span>
>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a9011-194">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a9011-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a9011-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Overdrive.</span><span class="sxs-lookup"><span data-stu-id="a9011-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Overdrive.</span></span>

![Assign User][200] 

<span data-ttu-id="a9011-197">**To assign Britta Simon to Overdrive, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9011-197">**To assign Britta Simon to Overdrive, perform the following steps:**</span></span>

1. <span data-ttu-id="a9011-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a9011-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="a9011-200">In the applications list, select **Overdrive**.</span><span class="sxs-lookup"><span data-stu-id="a9011-200">In the applications list, select **Overdrive**.</span></span>

    ![Configure Single Sign-On](./media/overdrive-books-tutorial/tutorial_overdrivebooks_app.png) 

1. <span data-ttu-id="a9011-202">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a9011-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="a9011-204">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a9011-204">Click **Add** button.</span></span> <span data-ttu-id="a9011-205">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a9011-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="a9011-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a9011-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="a9011-208">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a9011-208">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="a9011-209">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a9011-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a9011-210">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="a9011-210">Testing single sign-on</span></span>

<span data-ttu-id="a9011-211">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a9011-211">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a9011-212">When you click the Overdrive tile in the Access Panel, you should get automatically signed-on to your Overdrive application.</span><span class="sxs-lookup"><span data-stu-id="a9011-212">When you click the Overdrive tile in the Access Panel, you should get automatically signed-on to your Overdrive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a9011-213">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a9011-213">Additional resources</span></span>

* [<span data-ttu-id="a9011-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a9011-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a9011-215">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a9011-215">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/overdrive-books-tutorial/tutorial_general_01.png
[2]: ./media/overdrive-books-tutorial/tutorial_general_02.png
[3]: ./media/overdrive-books-tutorial/tutorial_general_03.png
[4]: ./media/overdrive-books-tutorial/tutorial_general_04.png

[100]: ./media/overdrive-books-tutorial/tutorial_general_100.png

[200]: ./media/overdrive-books-tutorial/tutorial_general_200.png
[201]: ./media/overdrive-books-tutorial/tutorial_general_201.png
[202]: ./media/overdrive-books-tutorial/tutorial_general_202.png
[203]: ./media/overdrive-books-tutorial/tutorial_general_203.png

