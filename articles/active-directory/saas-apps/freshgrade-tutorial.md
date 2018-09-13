---
title: 'Tutorial: Azure Active Directory integration with FreshGrade | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and FreshGrade.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1055bba6-f4df-462e-bc9b-1ad5ada0f638
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: jeedes
ms.openlocfilehash: c6439b31d2f8c95e0dc1526b92f21aee2966f12f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866750"
---
# <a name="tutorial-azure-active-directory-integration-with-freshgrade"></a><span data-ttu-id="210e9-103">Tutorial: Azure Active Directory integration with FreshGrade</span><span class="sxs-lookup"><span data-stu-id="210e9-103">Tutorial: Azure Active Directory integration with FreshGrade</span></span>

<span data-ttu-id="210e9-104">In this tutorial, you learn how to integrate FreshGrade with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="210e9-104">In this tutorial, you learn how to integrate FreshGrade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="210e9-105">Integrating FreshGrade with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="210e9-105">Integrating FreshGrade with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="210e9-106">You can control in Azure AD who has access to FreshGrade</span><span class="sxs-lookup"><span data-stu-id="210e9-106">You can control in Azure AD who has access to FreshGrade</span></span>
- <span data-ttu-id="210e9-107">You can enable your users to automatically get signed-on to FreshGrade (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="210e9-107">You can enable your users to automatically get signed-on to FreshGrade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="210e9-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="210e9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="210e9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="210e9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="210e9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="210e9-110">Prerequisites</span></span>

<span data-ttu-id="210e9-111">To configure Azure AD integration with FreshGrade, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="210e9-111">To configure Azure AD integration with FreshGrade, you need the following items:</span></span>

- <span data-ttu-id="210e9-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="210e9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="210e9-113">A FreshGrade single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="210e9-113">A FreshGrade single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="210e9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="210e9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="210e9-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="210e9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="210e9-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="210e9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="210e9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="210e9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="210e9-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="210e9-118">Scenario description</span></span>
<span data-ttu-id="210e9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="210e9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="210e9-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="210e9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="210e9-121">Adding FreshGrade from the gallery</span><span class="sxs-lookup"><span data-stu-id="210e9-121">Adding FreshGrade from the gallery</span></span>
1. <span data-ttu-id="210e9-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="210e9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshgrade-from-the-gallery"></a><span data-ttu-id="210e9-123">Adding FreshGrade from the gallery</span><span class="sxs-lookup"><span data-stu-id="210e9-123">Adding FreshGrade from the gallery</span></span>
<span data-ttu-id="210e9-124">To configure the integration of FreshGrade into Azure AD, you need to add FreshGrade from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="210e9-124">To configure the integration of FreshGrade into Azure AD, you need to add FreshGrade from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="210e9-125">**To add FreshGrade from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="210e9-125">**To add FreshGrade from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="210e9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="210e9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="210e9-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="210e9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="210e9-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="210e9-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="210e9-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="210e9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="210e9-133">In the search box, type **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="210e9-133">In the search box, type **FreshGrade**.</span></span>

    ![Creating an Azure AD test user](./media/freshgrade-tutorial/tutorial_freshgrade_search.png)

1. <span data-ttu-id="210e9-135">In the results panel, select **FreshGrade**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="210e9-135">In the results panel, select **FreshGrade**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/freshgrade-tutorial/tutorial_freshgrade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="210e9-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="210e9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="210e9-138">In this section, you configure and test Azure AD single sign-on with FreshGrade based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="210e9-138">In this section, you configure and test Azure AD single sign-on with FreshGrade based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="210e9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshGrade is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="210e9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshGrade is to a user in Azure AD.</span></span> <span data-ttu-id="210e9-140">In other words, a link relationship between an Azure AD user and the related user in FreshGrade needs to be established.</span><span class="sxs-lookup"><span data-stu-id="210e9-140">In other words, a link relationship between an Azure AD user and the related user in FreshGrade needs to be established.</span></span>

<span data-ttu-id="210e9-141">In FreshGrade, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="210e9-141">In FreshGrade, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="210e9-142">To configure and test Azure AD single sign-on with FreshGrade, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="210e9-142">To configure and test Azure AD single sign-on with FreshGrade, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="210e9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="210e9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="210e9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="210e9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="210e9-145">**[Creating a FreshGrade test user](#creating-a-freshgrade-test-user)** - to have a counterpart of Britta Simon in FreshGrade that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="210e9-145">**[Creating a FreshGrade test user](#creating-a-freshgrade-test-user)** - to have a counterpart of Britta Simon in FreshGrade that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="210e9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="210e9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="210e9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="210e9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="210e9-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="210e9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="210e9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FreshGrade application.</span><span class="sxs-lookup"><span data-stu-id="210e9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FreshGrade application.</span></span>

<span data-ttu-id="210e9-150">**To configure Azure AD single sign-on with FreshGrade, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="210e9-150">**To configure Azure AD single sign-on with FreshGrade, perform the following steps:**</span></span>

1. <span data-ttu-id="210e9-151">In the Azure portal, on the **FreshGrade** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="210e9-151">In the Azure portal, on the **FreshGrade** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="210e9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="210e9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configure Single Sign-On](./media/freshgrade-tutorial/tutorial_freshgrade_samlbase.png)

1. <span data-ttu-id="210e9-155">On the **FreshGrade Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="210e9-155">On the **FreshGrade Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/freshgrade-tutorial/tutorial_freshgrade_url.png)

    <span data-ttu-id="210e9-157">a.</span><span class="sxs-lookup"><span data-stu-id="210e9-157">a.</span></span> <span data-ttu-id="210e9-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span><span class="sxs-lookup"><span data-stu-id="210e9-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span>
      | |
      |--|
      | `https://<subdomain>.freshgrade.com/login` |
      | `https://<subdomain>.onboarding.freshgrade.com/login` |

    <span data-ttu-id="210e9-159">b.</span><span class="sxs-lookup"><span data-stu-id="210e9-159">b.</span></span> <span data-ttu-id="210e9-160">In the **Identifier** textbox, type a URL using the following patterns:</span><span class="sxs-lookup"><span data-stu-id="210e9-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span>
      | |
      |--|
      | `https://login.onboarding.freshgrade.com:443/saml/metadata/alias/<instancename>` |
      | `https://login.freshgrade.com:443/saml/metadata/alias/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="210e9-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="210e9-161">These values are not real.</span></span> <span data-ttu-id="210e9-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="210e9-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="210e9-163">Contact [FreshGrade Client support team](mailTo:support@freshgrade.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="210e9-163">Contact [FreshGrade Client support team](mailTo:support@freshgrade.com) to get these values.</span></span>

1. <span data-ttu-id="210e9-164">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="210e9-164">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>
    
    ![Configure Single Sign-On](./media/freshgrade-tutorial/tutorial_metadataurl.png)
     
1. <span data-ttu-id="210e9-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="210e9-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/freshgrade-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="210e9-168">On the **FreshGrade Configuration** section, click **Configure FreshGrade** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="210e9-168">On the **FreshGrade Configuration** section, click **Configure FreshGrade** to open **Configure sign-on** window.</span></span> <span data-ttu-id="210e9-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="210e9-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/freshgrade-tutorial/tutorial_freshgrade_configure.png)

1. <span data-ttu-id="210e9-171">To configure single sign-on on **FreshGrade** side, you need to send the **App Federation Metadata Url** and **SAML Single Sign-On Service URL** to [FreshGrade support team](mailTo:support@freshgrade.com).</span><span class="sxs-lookup"><span data-stu-id="210e9-171">To configure single sign-on on **FreshGrade** side, you need to send the **App Federation Metadata Url** and **SAML Single Sign-On Service URL** to [FreshGrade support team](mailTo:support@freshgrade.com).</span></span> <span data-ttu-id="210e9-172">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="210e9-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="210e9-173">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="210e9-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="210e9-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="210e9-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="210e9-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="210e9-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="210e9-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="210e9-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/freshgrade-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="210e9-179">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="210e9-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/freshgrade-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="210e9-181">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="210e9-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/freshgrade-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="210e9-183">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="210e9-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/freshgrade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="210e9-185">a.</span><span class="sxs-lookup"><span data-stu-id="210e9-185">a.</span></span> <span data-ttu-id="210e9-186">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="210e9-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="210e9-187">b.</span><span class="sxs-lookup"><span data-stu-id="210e9-187">b.</span></span> <span data-ttu-id="210e9-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="210e9-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="210e9-189">c.</span><span class="sxs-lookup"><span data-stu-id="210e9-189">c.</span></span> <span data-ttu-id="210e9-190">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="210e9-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="210e9-191">d.</span><span class="sxs-lookup"><span data-stu-id="210e9-191">d.</span></span> <span data-ttu-id="210e9-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="210e9-192">Click **Create**.</span></span>
 
### <a name="creating-a-freshgrade-test-user"></a><span data-ttu-id="210e9-193">Creating a FreshGrade test user</span><span class="sxs-lookup"><span data-stu-id="210e9-193">Creating a FreshGrade test user</span></span>

<span data-ttu-id="210e9-194">In this section, you create a user called Britta Simon in FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="210e9-194">In this section, you create a user called Britta Simon in FreshGrade.</span></span> <span data-ttu-id="210e9-195">Please work with [FreshGrade support team](mailTo:support@freshgrade.com) to add the users in the FreshGrade platform.</span><span class="sxs-lookup"><span data-stu-id="210e9-195">Please work with [FreshGrade support team](mailTo:support@freshgrade.com) to add the users in the FreshGrade platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="210e9-196">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="210e9-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="210e9-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="210e9-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FreshGrade.</span></span>

![Assign User][200] 

<span data-ttu-id="210e9-199">**To assign Britta Simon to FreshGrade, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="210e9-199">**To assign Britta Simon to FreshGrade, perform the following steps:**</span></span>

1. <span data-ttu-id="210e9-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="210e9-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="210e9-202">In the applications list, select **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="210e9-202">In the applications list, select **FreshGrade**.</span></span>

    ![Configure Single Sign-On](./media/freshgrade-tutorial/tutorial_freshgrade_app.png) 

1. <span data-ttu-id="210e9-204">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="210e9-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="210e9-206">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="210e9-206">Click **Add** button.</span></span> <span data-ttu-id="210e9-207">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="210e9-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="210e9-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="210e9-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="210e9-210">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="210e9-210">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="210e9-211">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="210e9-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="210e9-212">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="210e9-212">Testing single sign-on</span></span>

<span data-ttu-id="210e9-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="210e9-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="210e9-214">When you click the FreshGrade tile in the Access Panel, you should get automatically signed-on to your FreshGrade application.</span><span class="sxs-lookup"><span data-stu-id="210e9-214">When you click the FreshGrade tile in the Access Panel, you should get automatically signed-on to your FreshGrade application.</span></span>
<span data-ttu-id="210e9-215">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="210e9-215">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="210e9-216">Additional resources</span><span class="sxs-lookup"><span data-stu-id="210e9-216">Additional resources</span></span>

* [<span data-ttu-id="210e9-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="210e9-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="210e9-218">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="210e9-218">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/freshgrade-tutorial/tutorial_general_01.png
[2]: ./media/freshgrade-tutorial/tutorial_general_02.png
[3]: ./media/freshgrade-tutorial/tutorial_general_03.png
[4]: ./media/freshgrade-tutorial/tutorial_general_04.png

[100]: ./media/freshgrade-tutorial/tutorial_general_100.png

[200]: ./media/freshgrade-tutorial/tutorial_general_200.png
[201]: ./media/freshgrade-tutorial/tutorial_general_201.png
[202]: ./media/freshgrade-tutorial/tutorial_general_202.png
[203]: ./media/freshgrade-tutorial/tutorial_general_203.png

