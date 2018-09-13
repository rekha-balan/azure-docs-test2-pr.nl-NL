---
title: 'Tutorial: Azure Active Directory integration with Convercent | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Convercent.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9c9d290-0e13-490b-b559-0be772d6a690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: fcd1077719d3ebb10b1d43fe75e3feae2c3455a0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554526"
---
# <a name="tutorial-azure-active-directory-integration-with-convercent"></a><span data-ttu-id="88411-103">Tutorial: Azure Active Directory integration with Convercent</span><span class="sxs-lookup"><span data-stu-id="88411-103">Tutorial: Azure Active Directory integration with Convercent</span></span>

<span data-ttu-id="88411-104">In this tutorial, you learn how to integrate Convercent with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88411-104">In this tutorial, you learn how to integrate Convercent with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="88411-105">Integrating Convercent with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="88411-105">Integrating Convercent with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="88411-106">You can control in Azure AD who has access to Convercent</span><span class="sxs-lookup"><span data-stu-id="88411-106">You can control in Azure AD who has access to Convercent</span></span>
- <span data-ttu-id="88411-107">You can enable your users to automatically get signed-on to Convercent single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="88411-107">You can enable your users to automatically get signed-on to Convercent single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="88411-108">You can manage your accounts in one central location - the Azure new portal</span><span class="sxs-lookup"><span data-stu-id="88411-108">You can manage your accounts in one central location - the Azure new portal</span></span>

<span data-ttu-id="88411-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="88411-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88411-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="88411-110">Prerequisites</span></span>

<span data-ttu-id="88411-111">To configure Azure AD integration with Convercent, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="88411-111">To configure Azure AD integration with Convercent, you need the following items:</span></span>

- <span data-ttu-id="88411-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="88411-112">An Azure AD subscription</span></span>
- <span data-ttu-id="88411-113">A Convercent SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="88411-113">A Convercent SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="88411-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="88411-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="88411-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="88411-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="88411-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="88411-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="88411-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88411-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="88411-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="88411-118">Scenario description</span></span>
<span data-ttu-id="88411-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="88411-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="88411-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="88411-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="88411-121">Adding Convercent from the gallery</span><span class="sxs-lookup"><span data-stu-id="88411-121">Adding Convercent from the gallery</span></span>
2. <span data-ttu-id="88411-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="88411-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-convercent-from-the-gallery"></a><span data-ttu-id="88411-123">Add Convercent from the gallery</span><span class="sxs-lookup"><span data-stu-id="88411-123">Add Convercent from the gallery</span></span>
<span data-ttu-id="88411-124">To configure the integration of Convercent into Azure AD, you need to add Convercent from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="88411-124">To configure the integration of Convercent into Azure AD, you need to add Convercent from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="88411-125">**To add Convercent from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="88411-125">**To add Convercent from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="88411-126">In the **Azure Management portal**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="88411-126">In the **Azure Management portal**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="88411-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="88411-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="88411-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="88411-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="88411-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="88411-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="88411-133">In the search box, type **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="88411-133">In the search box, type **Convercent**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/tutorial_convercent_001.png)

5. <span data-ttu-id="88411-135">In the results panel, select **Convercent**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="88411-135">In the results panel, select **Convercent**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/tutorial_convercent_0001.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="88411-137">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="88411-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="88411-138">In this section, you configure and test Azure AD SSO with Convercent based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="88411-138">In this section, you configure and test Azure AD SSO with Convercent based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="88411-139">For SSO to work, Azure AD needs to know what the counterpart user in Convercent is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88411-139">For SSO to work, Azure AD needs to know what the counterpart user in Convercent is to a user in Azure AD.</span></span> <span data-ttu-id="88411-140">In other words, a link relationship between an Azure AD user and the related user in Convercent needs to be established.</span><span class="sxs-lookup"><span data-stu-id="88411-140">In other words, a link relationship between an Azure AD user and the related user in Convercent needs to be established.</span></span>

<span data-ttu-id="88411-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Convercent.</span><span class="sxs-lookup"><span data-stu-id="88411-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Convercent.</span></span>

<span data-ttu-id="88411-142">To configure and test Azure AD SSO with Convercent, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="88411-142">To configure and test Azure AD SSO with Convercent, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="88411-143">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="88411-143">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="88411-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88411-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="88411-145">**[Creating a Convercent test user](#creating-a-works-mobile-test-user)** - to have a counterpart of Britta Simon in Convercent that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="88411-145">**[Creating a Convercent test user](#creating-a-works-mobile-test-user)** - to have a counterpart of Britta Simon in Convercent that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="88411-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="88411-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="88411-147">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="88411-147">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="88411-148">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="88411-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="88411-149">In this section, you enable Azure AD SSO in the Azure new portal and configure single sign-on in your Convercent application.</span><span class="sxs-lookup"><span data-stu-id="88411-149">In this section, you enable Azure AD SSO in the Azure new portal and configure single sign-on in your Convercent application.</span></span>

<span data-ttu-id="88411-150">**To configure Azure AD single sign-on with Convercent, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="88411-150">**To configure Azure AD single sign-on with Convercent, perform the following steps:**</span></span>

1. <span data-ttu-id="88411-151">In the Azure new portal, on the **Convercent** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="88411-151">In the Azure new portal, on the **Convercent** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="88411-153">On the **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="88411-153">On the **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/tutorial_convercent_01.png)

3. <span data-ttu-id="88411-155">On the **Convercent Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="88411-155">On the **Convercent Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/tutorial_convercent_02.png)
  1. <span data-ttu-id="88411-157">In the **Identifier** textbox, type: `https://sts.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="88411-157">In the **Identifier** textbox, type: `https://sts.convercent.com/`</span></span>
  2. <span data-ttu-id="88411-158">Click **"Show advanced URL settings"**.</span><span class="sxs-lookup"><span data-stu-id="88411-158">Click **"Show advanced URL settings"**.</span></span>
  3. <span data-ttu-id="88411-159">In the **Relay State** textbox, type: `https://app.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="88411-159">In the **Relay State** textbox, type: `https://app.convercent.com/`</span></span>
    
4. <span data-ttu-id="88411-160">If you wish to configure the application in **SP initiated mode**, on the **Convercent Domain and URLs** section perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="88411-160">If you wish to configure the application in **SP initiated mode**, on the **Convercent Domain and URLs** section perform the following steps:</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/tutorial_convercent_03.png)
  * <span data-ttu-id="88411-162">In the **Sign On URL** textbox, type: `https://app.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="88411-162">In the **Sign On URL** textbox, type: `https://app.convercent.com/`</span></span>
    >[!NOTE] 
    ><span data-ttu-id="88411-163">Here we will suggest you to use the specified unique Identifier.</span><span class="sxs-lookup"><span data-stu-id="88411-163">Here we will suggest you to use the specified unique Identifier.</span></span> <span data-ttu-id="88411-164">Contact [Convercent support team](mailTo:support@convercent.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="88411-164">Contact [Convercent support team](mailTo:support@convercent.com) to get this value.</span></span>
    >

5. <span data-ttu-id="88411-165">On the **Convercent Configuration** section, click **Configure Convercent** to open **Configure sign-on** dialog.</span><span class="sxs-lookup"><span data-stu-id="88411-165">On the **Convercent Configuration** section, click **Configure Convercent** to open **Configure sign-on** dialog.</span></span> <span data-ttu-id="88411-166">Then click **SAML XML Metadata** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="88411-166">Then click **SAML XML Metadata** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/tutorial_convercent_04.png) 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/tutorial_convercent_05.png)

6. <span data-ttu-id="88411-169">To get SSO configured for your application, contact [Convercent support team](mailTo:support@convercent.com) and provide them with the downloaded **metadata**.</span><span class="sxs-lookup"><span data-stu-id="88411-169">To get SSO configured for your application, contact [Convercent support team](mailTo:support@convercent.com) and provide them with the downloaded **metadata**.</span></span>

7. <span data-ttu-id="88411-170">In the Azure new portal, click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="88411-170">In the Azure new portal, click **Save** button.</span></span>  
  
### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="88411-171">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="88411-171">Create an Azure AD test user</span></span>
<span data-ttu-id="88411-172">The objective of this section is to create a test user in the new portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88411-172">The objective of this section is to create a test user in the new portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="88411-174">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="88411-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="88411-175">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="88411-175">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="88411-177">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="88411-177">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="88411-179">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="88411-179">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="88411-181">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="88411-181">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/create_aaduser_04.png) 
 1. <span data-ttu-id="88411-183">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="88411-183">In the **Name** textbox, type **BrittaSimon**.</span></span>
 2. <span data-ttu-id="88411-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="88411-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>
 3. <span data-ttu-id="88411-185">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="88411-185">Select **Show Password** and write down the value of the **Password**.</span></span>
 4. <span data-ttu-id="88411-186">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="88411-186">Click **Create**.</span></span> 

### <a name="create-a-convercent-test-user"></a><span data-ttu-id="88411-187">Create a Convercent test user</span><span class="sxs-lookup"><span data-stu-id="88411-187">Create a Convercent test user</span></span>

<span data-ttu-id="88411-188">In this section, you create a user called Britta Simon in Convercent.</span><span class="sxs-lookup"><span data-stu-id="88411-188">In this section, you create a user called Britta Simon in Convercent.</span></span> <span data-ttu-id="88411-189">Please work with [Convercent support team](emailto:support@convercent.com) to add the users in the Convercent platform.</span><span class="sxs-lookup"><span data-stu-id="88411-189">Please work with [Convercent support team](emailto:support@convercent.com) to add the users in the Convercent platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="88411-190">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="88411-190">Assign the Azure AD test user</span></span>

<span data-ttu-id="88411-191">In this section, you enable Britta Simon to use Azure SSO by granting her access to Convercent.</span><span class="sxs-lookup"><span data-stu-id="88411-191">In this section, you enable Britta Simon to use Azure SSO by granting her access to Convercent.</span></span>

![Assign User][200] 

<span data-ttu-id="88411-193">**To assign Britta Simon to Convercent, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="88411-193">**To assign Britta Simon to Convercent, perform the following steps:**</span></span>

1. <span data-ttu-id="88411-194">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="88411-194">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="88411-196">In the applications list, select **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="88411-196">In the applications list, select **Convercent**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/tutorial_convercent_50.png) 

3. <span data-ttu-id="88411-198">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="88411-198">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="88411-200">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="88411-200">Click **Add** button.</span></span> <span data-ttu-id="88411-201">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="88411-201">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="88411-203">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="88411-203">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="88411-204">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="88411-204">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="88411-205">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="88411-205">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="88411-206">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="88411-206">Test single sign-on</span></span>

<span data-ttu-id="88411-207">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="88411-207">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="88411-208">When you click the Convercent tile in the Access Panel, you should get automatically signed-on to your Convercent application.</span><span class="sxs-lookup"><span data-stu-id="88411-208">When you click the Convercent tile in the Access Panel, you should get automatically signed-on to your Convercent application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="88411-209">Additional resources</span><span class="sxs-lookup"><span data-stu-id="88411-209">Additional resources</span></span>

* [<span data-ttu-id="88411-210">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88411-210">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="88411-211">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="88411-211">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-convercent-tutorial/tutorial_general_203.png




















