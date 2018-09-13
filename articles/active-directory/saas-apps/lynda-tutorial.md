---
title: 'Tutorial: Azure Active Directory integration with Lynda.com | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Lynda.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 12f61e30321514b6e1283e04c5723d9fe2a4e054
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865501"
---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a><span data-ttu-id="deda7-103">Tutorial: Azure Active Directory integration with Lynda.com</span><span class="sxs-lookup"><span data-stu-id="deda7-103">Tutorial: Azure Active Directory integration with Lynda.com</span></span>

<span data-ttu-id="deda7-104">In this tutorial, you learn how to integrate Lynda.com with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="deda7-104">In this tutorial, you learn how to integrate Lynda.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="deda7-105">Integrating Lynda.com with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="deda7-105">Integrating Lynda.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="deda7-106">You can control in Azure AD who has access to Lynda.com</span><span class="sxs-lookup"><span data-stu-id="deda7-106">You can control in Azure AD who has access to Lynda.com</span></span>
- <span data-ttu-id="deda7-107">You can enable your users to automatically get signed-on to Lynda.com (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="deda7-107">You can enable your users to automatically get signed-on to Lynda.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="deda7-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="deda7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="deda7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="deda7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="deda7-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="deda7-110">Prerequisites</span></span>

<span data-ttu-id="deda7-111">To configure Azure AD integration with Lynda.com, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="deda7-111">To configure Azure AD integration with Lynda.com, you need the following items:</span></span>

- <span data-ttu-id="deda7-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="deda7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="deda7-113">A Lynda.com single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="deda7-113">A Lynda.com single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="deda7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="deda7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="deda7-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="deda7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="deda7-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="deda7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="deda7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="deda7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="deda7-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="deda7-118">Scenario description</span></span>
<span data-ttu-id="deda7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="deda7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="deda7-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="deda7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="deda7-121">Adding Lynda.com from the gallery</span><span class="sxs-lookup"><span data-stu-id="deda7-121">Adding Lynda.com from the gallery</span></span>
1. <span data-ttu-id="deda7-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="deda7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lyndacom-from-the-gallery"></a><span data-ttu-id="deda7-123">Adding Lynda.com from the gallery</span><span class="sxs-lookup"><span data-stu-id="deda7-123">Adding Lynda.com from the gallery</span></span>
<span data-ttu-id="deda7-124">To configure the integration of Lynda.com into Azure AD, you need to add Lynda.com from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="deda7-124">To configure the integration of Lynda.com into Azure AD, you need to add Lynda.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="deda7-125">**To add Lynda.com from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="deda7-125">**To add Lynda.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="deda7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="deda7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="deda7-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="deda7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="deda7-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="deda7-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="deda7-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="deda7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="deda7-133">In the search box, type **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="deda7-133">In the search box, type **Lynda.com**.</span></span>

    ![Creating an Azure AD test user](./media/lynda-tutorial/tutorial_lynda.com_search.png)

1. <span data-ttu-id="deda7-135">In the results panel, select **Lynda.com**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="deda7-135">In the results panel, select **Lynda.com**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/lynda-tutorial/tutorial_lynda.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="deda7-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="deda7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="deda7-138">In this section, you configure and test Azure AD single sign-on with Lynda.com based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="deda7-138">In this section, you configure and test Azure AD single sign-on with Lynda.com based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="deda7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lynda.com is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="deda7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lynda.com is to a user in Azure AD.</span></span> <span data-ttu-id="deda7-140">In other words, a link relationship between an Azure AD user and the related user in Lynda.com needs to be established.</span><span class="sxs-lookup"><span data-stu-id="deda7-140">In other words, a link relationship between an Azure AD user and the related user in Lynda.com needs to be established.</span></span>

<span data-ttu-id="deda7-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="deda7-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lynda.com.</span></span>

<span data-ttu-id="deda7-142">To configure and test Azure AD single sign-on with Lynda.com, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="deda7-142">To configure and test Azure AD single sign-on with Lynda.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="deda7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="deda7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="deda7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="deda7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="deda7-145">**[Creating a Lynda.com test user](#creating-a-lyndacom-test-user)** - to have a counterpart of Britta Simon in Lynda.com that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="deda7-145">**[Creating a Lynda.com test user](#creating-a-lyndacom-test-user)** - to have a counterpart of Britta Simon in Lynda.com that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="deda7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="deda7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="deda7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="deda7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="deda7-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="deda7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="deda7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lynda.com application.</span><span class="sxs-lookup"><span data-stu-id="deda7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lynda.com application.</span></span>

<span data-ttu-id="deda7-150">**To configure Azure AD single sign-on with Lynda.com, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="deda7-150">**To configure Azure AD single sign-on with Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="deda7-151">In the Azure portal, on the **Lynda.com** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="deda7-151">In the Azure portal, on the **Lynda.com** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="deda7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="deda7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/lynda-tutorial/tutorial_lynda.com_samlbase.png)

1. <span data-ttu-id="deda7-155">On the **Lynda.com Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="deda7-155">On the **Lynda.com Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/lynda-tutorial/tutorial_lynda.com_url.png)

    <span data-ttu-id="deda7-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span><span class="sxs-lookup"><span data-stu-id="deda7-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="deda7-158">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="deda7-158">This value is not real.</span></span> <span data-ttu-id="deda7-159">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="deda7-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="deda7-160">Contact [Lynda.com Client support team](https://www.linkedin.com/help/lynda/ask) to get these values.</span><span class="sxs-lookup"><span data-stu-id="deda7-160">Contact [Lynda.com Client support team](https://www.linkedin.com/help/lynda/ask) to get these values.</span></span> 
 
1. <span data-ttu-id="deda7-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="deda7-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](./media/lynda-tutorial/tutorial_lynda.com_certificate.png) 

1. <span data-ttu-id="deda7-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="deda7-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/lynda-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="deda7-165">To configure single sign-on on **Lynda.com** side, you need to send the downloaded **Metadata XML** [Lynda.com support](https://www.linkedin.com/help/lynda/ask).</span><span class="sxs-lookup"><span data-stu-id="deda7-165">To configure single sign-on on **Lynda.com** side, you need to send the downloaded **Metadata XML** [Lynda.com support](https://www.linkedin.com/help/lynda/ask).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="deda7-166">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="deda7-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="deda7-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="deda7-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="deda7-169">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="deda7-169">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="deda7-170">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="deda7-170">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/lynda-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="deda7-172">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="deda7-172">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/lynda-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="deda7-174">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="deda7-174">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/lynda-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="deda7-176">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="deda7-176">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/lynda-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="deda7-178">a.</span><span class="sxs-lookup"><span data-stu-id="deda7-178">a.</span></span> <span data-ttu-id="deda7-179">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="deda7-179">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="deda7-180">b.</span><span class="sxs-lookup"><span data-stu-id="deda7-180">b.</span></span> <span data-ttu-id="deda7-181">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="deda7-181">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="deda7-182">c.</span><span class="sxs-lookup"><span data-stu-id="deda7-182">c.</span></span> <span data-ttu-id="deda7-183">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="deda7-183">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="deda7-184">d.</span><span class="sxs-lookup"><span data-stu-id="deda7-184">d.</span></span> <span data-ttu-id="deda7-185">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="deda7-185">Click **Create**.</span></span>
 
### <a name="creating-a-lyndacom-test-user"></a><span data-ttu-id="deda7-186">Creating a Lynda.com test user</span><span class="sxs-lookup"><span data-stu-id="deda7-186">Creating a Lynda.com test user</span></span>

<span data-ttu-id="deda7-187">There is no action item for you to configure user provisioning to Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="deda7-187">There is no action item for you to configure user provisioning to Lynda.com.</span></span>  
<span data-ttu-id="deda7-188">When an assigned user tries to log in to Lynda.com using the access panel, Lynda.com checks whether the user exists.</span><span class="sxs-lookup"><span data-stu-id="deda7-188">When an assigned user tries to log in to Lynda.com using the access panel, Lynda.com checks whether the user exists.</span></span>  

<span data-ttu-id="deda7-189">If there is no user account available yet, it is automatically created by Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="deda7-189">If there is no user account available yet, it is automatically created by Lynda.com.</span></span>

>[!NOTE]
><span data-ttu-id="deda7-190">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="deda7-190">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="deda7-191">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="deda7-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="deda7-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="deda7-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lynda.com.</span></span>

![Assign User][200] 

<span data-ttu-id="deda7-194">**To assign Britta Simon to Lynda.com, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="deda7-194">**To assign Britta Simon to Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="deda7-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="deda7-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="deda7-197">In the applications list, select **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="deda7-197">In the applications list, select **Lynda.com**.</span></span>

    ![Configure Single Sign-On](./media/lynda-tutorial/tutorial_lynda.com_app.png) 

1. <span data-ttu-id="deda7-199">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="deda7-199">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="deda7-201">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="deda7-201">Click **Add** button.</span></span> <span data-ttu-id="deda7-202">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="deda7-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="deda7-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="deda7-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="deda7-205">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="deda7-205">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="deda7-206">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="deda7-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="deda7-207">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="deda7-207">Testing single sign-on</span></span>

<span data-ttu-id="deda7-208">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="deda7-208">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="deda7-209">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="deda7-209">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="deda7-210">Additional resources</span><span class="sxs-lookup"><span data-stu-id="deda7-210">Additional resources</span></span>

* [<span data-ttu-id="deda7-211">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="deda7-211">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="deda7-212">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="deda7-212">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/lynda-tutorial/tutorial_general_01.png
[2]: ./media/lynda-tutorial/tutorial_general_02.png
[3]: ./media/lynda-tutorial/tutorial_general_03.png
[4]: ./media/lynda-tutorial/tutorial_general_04.png

[100]: ./media/lynda-tutorial/tutorial_general_100.png

[200]: ./media/lynda-tutorial/tutorial_general_200.png
[201]: ./media/lynda-tutorial/tutorial_general_201.png
[202]: ./media/lynda-tutorial/tutorial_general_202.png
[203]: ./media/lynda-tutorial/tutorial_general_203.png

