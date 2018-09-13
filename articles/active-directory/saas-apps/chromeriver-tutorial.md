---
title: 'Tutorial: Azure Active Directory integration with Chromeriver | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Chromeriver.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 445c5600-e340-4724-a9cb-3cfaf5770b70
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: 7c69b4319bfa1b89561deb14a580a77d000c11c7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857535"
---
# <a name="tutorial-azure-active-directory-integration-with-chromeriver"></a><span data-ttu-id="6eb32-103">Tutorial: Azure Active Directory integration with Chromeriver</span><span class="sxs-lookup"><span data-stu-id="6eb32-103">Tutorial: Azure Active Directory integration with Chromeriver</span></span>

<span data-ttu-id="6eb32-104">In this tutorial, you learn how to integrate Chromeriver with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6eb32-104">In this tutorial, you learn how to integrate Chromeriver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6eb32-105">Integrating Chromeriver with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="6eb32-105">Integrating Chromeriver with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6eb32-106">You can control in Azure AD who has access to Chromeriver</span><span class="sxs-lookup"><span data-stu-id="6eb32-106">You can control in Azure AD who has access to Chromeriver</span></span>
- <span data-ttu-id="6eb32-107">You can enable your users to automatically get signed-on to Chromeriver (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="6eb32-107">You can enable your users to automatically get signed-on to Chromeriver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6eb32-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6eb32-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6eb32-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="6eb32-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6eb32-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6eb32-110">Prerequisites</span></span>

<span data-ttu-id="6eb32-111">To configure Azure AD integration with Chromeriver, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="6eb32-111">To configure Azure AD integration with Chromeriver, you need the following items:</span></span>

- <span data-ttu-id="6eb32-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="6eb32-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6eb32-113">A Chromeriver single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="6eb32-113">A Chromeriver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6eb32-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="6eb32-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6eb32-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="6eb32-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6eb32-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="6eb32-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6eb32-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6eb32-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6eb32-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="6eb32-118">Scenario description</span></span>
<span data-ttu-id="6eb32-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="6eb32-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6eb32-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="6eb32-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6eb32-121">Adding Chromeriver from the gallery</span><span class="sxs-lookup"><span data-stu-id="6eb32-121">Adding Chromeriver from the gallery</span></span>
1. <span data-ttu-id="6eb32-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6eb32-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-chromeriver-from-the-gallery"></a><span data-ttu-id="6eb32-123">Adding Chromeriver from the gallery</span><span class="sxs-lookup"><span data-stu-id="6eb32-123">Adding Chromeriver from the gallery</span></span>
<span data-ttu-id="6eb32-124">To configure the integration of Chromeriver into Azure AD, you need to add Chromeriver from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="6eb32-124">To configure the integration of Chromeriver into Azure AD, you need to add Chromeriver from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6eb32-125">**To add Chromeriver from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6eb32-125">**To add Chromeriver from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6eb32-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="6eb32-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="6eb32-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="6eb32-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6eb32-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6eb32-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="6eb32-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="6eb32-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="6eb32-133">In the search box, type **Chromeriver**.</span><span class="sxs-lookup"><span data-stu-id="6eb32-133">In the search box, type **Chromeriver**.</span></span>

    ![Creating an Azure AD test user](./media/chromeriver-tutorial/tutorial_chromeriver_search.png)

1. <span data-ttu-id="6eb32-135">In the results panel, select **Chromeriver**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="6eb32-135">In the results panel, select **Chromeriver**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/chromeriver-tutorial/tutorial_chromeriver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6eb32-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6eb32-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6eb32-138">In this section, you configure and test Azure AD single sign-on with Chromeriver based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="6eb32-138">In this section, you configure and test Azure AD single sign-on with Chromeriver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6eb32-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Chromeriver is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6eb32-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Chromeriver is to a user in Azure AD.</span></span> <span data-ttu-id="6eb32-140">In other words, a link relationship between an Azure AD user and the related user in Chromeriver needs to be established.</span><span class="sxs-lookup"><span data-stu-id="6eb32-140">In other words, a link relationship between an Azure AD user and the related user in Chromeriver needs to be established.</span></span>

<span data-ttu-id="6eb32-141">In Chromeriver, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="6eb32-141">In Chromeriver, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6eb32-142">To configure and test Azure AD single sign-on with Chromeriver, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6eb32-142">To configure and test Azure AD single sign-on with Chromeriver, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6eb32-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="6eb32-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="6eb32-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6eb32-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="6eb32-145">**[Creating a Chromeriver test user](#creating-a-chromeriver-test-user)** - to have a counterpart of Britta Simon in Chromeriver that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="6eb32-145">**[Creating a Chromeriver test user](#creating-a-chromeriver-test-user)** - to have a counterpart of Britta Simon in Chromeriver that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="6eb32-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6eb32-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="6eb32-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="6eb32-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6eb32-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6eb32-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6eb32-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Chromeriver application.</span><span class="sxs-lookup"><span data-stu-id="6eb32-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Chromeriver application.</span></span>

<span data-ttu-id="6eb32-150">**To configure Azure AD single sign-on with Chromeriver, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6eb32-150">**To configure Azure AD single sign-on with Chromeriver, perform the following steps:**</span></span>

1. <span data-ttu-id="6eb32-151">In the Azure portal, on the **Chromeriver** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6eb32-151">In the Azure portal, on the **Chromeriver** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="6eb32-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6eb32-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/chromeriver-tutorial/tutorial_chromeriver_samlbase.png)

1. <span data-ttu-id="6eb32-155">On the **Chromeriver Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6eb32-155">On the **Chromeriver Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/chromeriver-tutorial/tutorial_chromeriver_url.png)

    <span data-ttu-id="6eb32-157">a.</span><span class="sxs-lookup"><span data-stu-id="6eb32-157">a.</span></span> <span data-ttu-id="6eb32-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.chromeriver.com`</span><span class="sxs-lookup"><span data-stu-id="6eb32-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.chromeriver.com`</span></span>

    <span data-ttu-id="6eb32-159">b.</span><span class="sxs-lookup"><span data-stu-id="6eb32-159">b.</span></span> <span data-ttu-id="6eb32-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.chromeriver.com/login/sso/saml/consume?customerId=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="6eb32-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.chromeriver.com/login/sso/saml/consume?customerId=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6eb32-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="6eb32-161">These values are not real.</span></span> <span data-ttu-id="6eb32-162">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="6eb32-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="6eb32-163">Contact [Chromeriver support team](https://www.chromeriver.com/services/support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="6eb32-163">Contact [Chromeriver support team](https://www.chromeriver.com/services/support) to get these values.</span></span>
 


1. <span data-ttu-id="6eb32-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="6eb32-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/chromeriver-tutorial/tutorial_chromeriver_certificate.png) 

1. <span data-ttu-id="6eb32-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="6eb32-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/chromeriver-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="6eb32-168">To configure single sign-on on **Chromeriver** side, you need to send the downloaded **Metadata XML** to [Chromeriver support team](https://www.chromeriver.com/services/support).</span><span class="sxs-lookup"><span data-stu-id="6eb32-168">To configure single sign-on on **Chromeriver** side, you need to send the downloaded **Metadata XML** to [Chromeriver support team](https://www.chromeriver.com/services/support).</span></span> <span data-ttu-id="6eb32-169">You will get a notification when SSO has been enabled for your subscription.</span><span class="sxs-lookup"><span data-stu-id="6eb32-169">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="6eb32-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="6eb32-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6eb32-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="6eb32-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6eb32-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6eb32-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6eb32-173">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6eb32-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="6eb32-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6eb32-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="6eb32-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6eb32-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6eb32-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="6eb32-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/chromeriver-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="6eb32-179">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="6eb32-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/chromeriver-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="6eb32-181">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="6eb32-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/chromeriver-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="6eb32-183">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6eb32-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/chromeriver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6eb32-185">a.</span><span class="sxs-lookup"><span data-stu-id="6eb32-185">a.</span></span> <span data-ttu-id="6eb32-186">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6eb32-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6eb32-187">b.</span><span class="sxs-lookup"><span data-stu-id="6eb32-187">b.</span></span> <span data-ttu-id="6eb32-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6eb32-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6eb32-189">c.</span><span class="sxs-lookup"><span data-stu-id="6eb32-189">c.</span></span> <span data-ttu-id="6eb32-190">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="6eb32-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6eb32-191">d.</span><span class="sxs-lookup"><span data-stu-id="6eb32-191">d.</span></span> <span data-ttu-id="6eb32-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6eb32-192">Click **Create**.</span></span>
 
### <a name="creating-a-chromeriver-test-user"></a><span data-ttu-id="6eb32-193">Creating a Chromeriver test user</span><span class="sxs-lookup"><span data-stu-id="6eb32-193">Creating a Chromeriver test user</span></span>

<span data-ttu-id="6eb32-194">To enable Azure AD users to log in to Chromeriver, they must be provisioned into Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="6eb32-194">To enable Azure AD users to log in to Chromeriver, they must be provisioned into Chromeriver.</span></span>  

<span data-ttu-id="6eb32-195">In the case of Chromeriver, the user accounts need to be created by your [Chromeriver support team](https://www.chromeriver.com/services/support).</span><span class="sxs-lookup"><span data-stu-id="6eb32-195">In the case of Chromeriver, the user accounts need to be created by your [Chromeriver support team](https://www.chromeriver.com/services/support).</span></span>

>[!NOTE]
><span data-ttu-id="6eb32-196">You can use any other Chromeriver user account creation tools or APIs provided by Chromeriver to provision Azure Active Directory user accounts.</span><span class="sxs-lookup"><span data-stu-id="6eb32-196">You can use any other Chromeriver user account creation tools or APIs provided by Chromeriver to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6eb32-197">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6eb32-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6eb32-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="6eb32-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Chromeriver.</span></span>

![Assign User][200] 

<span data-ttu-id="6eb32-200">**To assign Britta Simon to Chromeriver, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6eb32-200">**To assign Britta Simon to Chromeriver, perform the following steps:**</span></span>

1. <span data-ttu-id="6eb32-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6eb32-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="6eb32-203">In the applications list, select **Chromeriver**.</span><span class="sxs-lookup"><span data-stu-id="6eb32-203">In the applications list, select **Chromeriver**.</span></span>

    ![Configure Single Sign-On](./media/chromeriver-tutorial/tutorial_chromeriver_app.png) 

1. <span data-ttu-id="6eb32-205">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="6eb32-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="6eb32-207">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="6eb32-207">Click **Add** button.</span></span> <span data-ttu-id="6eb32-208">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6eb32-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="6eb32-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="6eb32-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="6eb32-211">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="6eb32-211">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="6eb32-212">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6eb32-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6eb32-213">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="6eb32-213">Testing single sign-on</span></span>

<span data-ttu-id="6eb32-214">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="6eb32-214">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6eb32-215">When you click the Chromeriver tile in the Access Panel, you should get automatically signed-on to your Chromeriver application.</span><span class="sxs-lookup"><span data-stu-id="6eb32-215">When you click the Chromeriver tile in the Access Panel, you should get automatically signed-on to your Chromeriver application.</span></span> <span data-ttu-id="6eb32-216">For more details about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6eb32-216">For more details about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6eb32-217">Additional resources</span><span class="sxs-lookup"><span data-stu-id="6eb32-217">Additional resources</span></span>

* [<span data-ttu-id="6eb32-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6eb32-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="6eb32-219">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6eb32-219">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/chromeriver-tutorial/tutorial_general_01.png
[2]: ./media/chromeriver-tutorial/tutorial_general_02.png
[3]: ./media/chromeriver-tutorial/tutorial_general_03.png
[4]: ./media/chromeriver-tutorial/tutorial_general_04.png

[100]: ./media/chromeriver-tutorial/tutorial_general_100.png

[200]: ./media/chromeriver-tutorial/tutorial_general_200.png
[201]: ./media/chromeriver-tutorial/tutorial_general_201.png
[202]: ./media/chromeriver-tutorial/tutorial_general_202.png
[203]: ./media/chromeriver-tutorial/tutorial_general_203.png
