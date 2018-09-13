---
title: 'Tutorial: Azure Active Directory integration with Inkling | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Inkling.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 64c7ee45-ee8a-42f7-bf04-fd0e00833ea9
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: cd7f8871cedb36157f3a16f093b09073576fe56e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868223"
---
# <a name="tutorial-azure-active-directory-integration-with-inkling"></a><span data-ttu-id="6fecc-103">Tutorial: Azure Active Directory integration with Inkling</span><span class="sxs-lookup"><span data-stu-id="6fecc-103">Tutorial: Azure Active Directory integration with Inkling</span></span>

<span data-ttu-id="6fecc-104">In this tutorial, you learn how to integrate Inkling with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6fecc-104">In this tutorial, you learn how to integrate Inkling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6fecc-105">Integrating Inkling with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="6fecc-105">Integrating Inkling with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6fecc-106">You can control in Azure AD who has access to Inkling</span><span class="sxs-lookup"><span data-stu-id="6fecc-106">You can control in Azure AD who has access to Inkling</span></span>
- <span data-ttu-id="6fecc-107">You can enable your users to automatically get signed-on to Inkling (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="6fecc-107">You can enable your users to automatically get signed-on to Inkling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6fecc-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="6fecc-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="6fecc-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="6fecc-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fecc-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6fecc-110">Prerequisites</span></span>

<span data-ttu-id="6fecc-111">To configure Azure AD integration with Inkling, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="6fecc-111">To configure Azure AD integration with Inkling, you need the following items:</span></span>

- <span data-ttu-id="6fecc-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="6fecc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6fecc-113">An Inkling single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="6fecc-113">An Inkling single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="6fecc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="6fecc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="6fecc-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="6fecc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6fecc-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="6fecc-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="6fecc-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6fecc-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="6fecc-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="6fecc-118">Scenario description</span></span>
<span data-ttu-id="6fecc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="6fecc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6fecc-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="6fecc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6fecc-121">Adding Inkling from the gallery</span><span class="sxs-lookup"><span data-stu-id="6fecc-121">Adding Inkling from the gallery</span></span>
1. <span data-ttu-id="6fecc-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6fecc-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-inkling-from-the-gallery"></a><span data-ttu-id="6fecc-123">Adding Inkling from the gallery</span><span class="sxs-lookup"><span data-stu-id="6fecc-123">Adding Inkling from the gallery</span></span>
<span data-ttu-id="6fecc-124">To configure the integration of Inkling into Azure AD, you need to add Inkling from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="6fecc-124">To configure the integration of Inkling into Azure AD, you need to add Inkling from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6fecc-125">**To add Inkling from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6fecc-125">**To add Inkling from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6fecc-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="6fecc-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="6fecc-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="6fecc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6fecc-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6fecc-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="6fecc-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="6fecc-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="6fecc-133">In the search box, type **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="6fecc-133">In the search box, type **Inkling**.</span></span>

    ![Creating an Azure AD test user](./media/inkling-tutorial/tutorial_inkling_001.png)

1. <span data-ttu-id="6fecc-135">In the results panel, select **Inkling**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="6fecc-135">In the results panel, select **Inkling**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/inkling-tutorial/tutorial_inkling_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6fecc-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6fecc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6fecc-138">In this section, you configure and test Azure AD single sign-on with Inkling based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6fecc-138">In this section, you configure and test Azure AD single sign-on with Inkling based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6fecc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Inkling is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6fecc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Inkling is to a user in Azure AD.</span></span> <span data-ttu-id="6fecc-140">In other words, a link relationship between an Azure AD user and the related user in Inkling needs to be established.</span><span class="sxs-lookup"><span data-stu-id="6fecc-140">In other words, a link relationship between an Azure AD user and the related user in Inkling needs to be established.</span></span>

<span data-ttu-id="6fecc-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Inkling.</span><span class="sxs-lookup"><span data-stu-id="6fecc-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Inkling.</span></span>

<span data-ttu-id="6fecc-142">To configure and test Azure AD single sign-on with Inkling, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6fecc-142">To configure and test Azure AD single sign-on with Inkling, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6fecc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="6fecc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="6fecc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6fecc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="6fecc-145">**[Creating an Inkling test user](#creating-an-inkling-test-user)** - to have a counterpart of Britta Simon in Inkling that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="6fecc-145">**[Creating an Inkling test user](#creating-an-inkling-test-user)** - to have a counterpart of Britta Simon in Inkling that is linked to the Azure AD representation of her.</span></span>
1. <span data-ttu-id="6fecc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6fecc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="6fecc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="6fecc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6fecc-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6fecc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6fecc-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Inkling application.</span><span class="sxs-lookup"><span data-stu-id="6fecc-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Inkling application.</span></span>

<span data-ttu-id="6fecc-150">**To configure Azure AD single sign-on with Inkling, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6fecc-150">**To configure Azure AD single sign-on with Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="6fecc-151">In the Azure Management portal, on the **Inkling** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6fecc-151">In the Azure Management portal, on the **Inkling** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="6fecc-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="6fecc-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](./media/inkling-tutorial/tutorial_general_300.png)
    
1. <span data-ttu-id="6fecc-155">On the **Inkling Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6fecc-155">On the **Inkling Domain and URLs** section, perform the following steps:</span></span>
    
    ![Configure Single Sign-On](./media/inkling-tutorial/tutorial_inkling_01.png)

    <span data-ttu-id="6fecc-157">a.</span><span class="sxs-lookup"><span data-stu-id="6fecc-157">a.</span></span> <span data-ttu-id="6fecc-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="6fecc-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span></span>

    <span data-ttu-id="6fecc-159">b.</span><span class="sxs-lookup"><span data-stu-id="6fecc-159">b.</span></span> <span data-ttu-id="6fecc-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/acs/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="6fecc-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/acs/<user-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6fecc-161">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="6fecc-161">Please note that these are not the real values.</span></span> <span data-ttu-id="6fecc-162">You have to update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="6fecc-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="6fecc-163">Contact [Inkling support team](mailto:press@inkling.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="6fecc-163">Contact [Inkling support team](mailto:press@inkling.com) to get these values.</span></span>

1. <span data-ttu-id="6fecc-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="6fecc-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configure Single Sign-On](./media/inkling-tutorial/tutorial_general_400.png)  

1. <span data-ttu-id="6fecc-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span><span class="sxs-lookup"><span data-stu-id="6fecc-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="6fecc-167">Then click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="6fecc-167">Then click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/inkling-tutorial/tutorial_general_500.png)

1. <span data-ttu-id="6fecc-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="6fecc-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/inkling-tutorial/tutorial_inkling_02.png)

1. <span data-ttu-id="6fecc-171">On the pop-up **Rollover certificate** window, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="6fecc-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configure Single Sign-On](./media/inkling-tutorial/tutorial_general_600.png)

1. <span data-ttu-id="6fecc-173">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="6fecc-173">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/inkling-tutorial/tutorial_inkling_03.png) 

1. <span data-ttu-id="6fecc-175">To get SSO configured for your application, contact [Inkling support team](mailto:press@inkling.com) and provide them with downloaded **metadata**.</span><span class="sxs-lookup"><span data-stu-id="6fecc-175">To get SSO configured for your application, contact [Inkling support team](mailto:press@inkling.com) and provide them with downloaded **metadata**.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6fecc-176">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6fecc-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="6fecc-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6fecc-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="6fecc-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6fecc-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6fecc-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="6fecc-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/inkling-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="6fecc-182">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="6fecc-182">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](./media/inkling-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="6fecc-184">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="6fecc-184">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/inkling-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="6fecc-186">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6fecc-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/inkling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6fecc-188">a.</span><span class="sxs-lookup"><span data-stu-id="6fecc-188">a.</span></span> <span data-ttu-id="6fecc-189">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6fecc-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6fecc-190">b.</span><span class="sxs-lookup"><span data-stu-id="6fecc-190">b.</span></span> <span data-ttu-id="6fecc-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6fecc-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6fecc-192">c.</span><span class="sxs-lookup"><span data-stu-id="6fecc-192">c.</span></span> <span data-ttu-id="6fecc-193">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="6fecc-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6fecc-194">d.</span><span class="sxs-lookup"><span data-stu-id="6fecc-194">d.</span></span> <span data-ttu-id="6fecc-195">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6fecc-195">Click **Create**.</span></span> 



### <a name="creating-an-inkling-test-user"></a><span data-ttu-id="6fecc-196">Creating an Inkling test user</span><span class="sxs-lookup"><span data-stu-id="6fecc-196">Creating an Inkling test user</span></span>

<span data-ttu-id="6fecc-197">In this section, you create a user called Britta Simon in Inkling.</span><span class="sxs-lookup"><span data-stu-id="6fecc-197">In this section, you create a user called Britta Simon in Inkling.</span></span> <span data-ttu-id="6fecc-198">Please work with [Inkling support team](mailto:press@inkling.com) to add the users in the Inkling platform.</span><span class="sxs-lookup"><span data-stu-id="6fecc-198">Please work with [Inkling support team](mailto:press@inkling.com) to add the users in the Inkling platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6fecc-199">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6fecc-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6fecc-200">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Inkling.</span><span class="sxs-lookup"><span data-stu-id="6fecc-200">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Inkling.</span></span>

![Assign User][200] 

<span data-ttu-id="6fecc-202">**To assign Britta Simon to Inkling, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6fecc-202">**To assign Britta Simon to Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="6fecc-203">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6fecc-203">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="6fecc-205">In the applications list, select **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="6fecc-205">In the applications list, select **Inkling**.</span></span>

    ![Configure Single Sign-On](./media/inkling-tutorial/tutorial_inkling_50.png) 

1. <span data-ttu-id="6fecc-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="6fecc-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="6fecc-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="6fecc-209">Click **Add** button.</span></span> <span data-ttu-id="6fecc-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6fecc-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="6fecc-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="6fecc-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="6fecc-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="6fecc-213">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="6fecc-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6fecc-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="6fecc-215">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="6fecc-215">Testing single sign-on</span></span>

<span data-ttu-id="6fecc-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="6fecc-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6fecc-217">When you click the Inkling tile in the Access Panel, you should get automatically signed-on to your Inkling application.</span><span class="sxs-lookup"><span data-stu-id="6fecc-217">When you click the Inkling tile in the Access Panel, you should get automatically signed-on to your Inkling application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="6fecc-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="6fecc-218">Additional resources</span></span>

* [<span data-ttu-id="6fecc-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6fecc-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="6fecc-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6fecc-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/inkling-tutorial/tutorial_general_01.png
[2]: ./media/inkling-tutorial/tutorial_general_02.png
[3]: ./media/inkling-tutorial/tutorial_general_03.png
[4]: ./media/inkling-tutorial/tutorial_general_04.png

[100]: ./media/inkling-tutorial/tutorial_general_100.png

[200]: ./media/inkling-tutorial/tutorial_general_200.png
[201]: ./media/inkling-tutorial/tutorial_general_201.png
[202]: ./media/inkling-tutorial/tutorial_general_202.png
[203]: ./media/inkling-tutorial/tutorial_general_203.png