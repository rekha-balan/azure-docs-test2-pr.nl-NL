---
title: 'Tutorial: Azure Active Directory integration with Inkling | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Inkling.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 64c7ee45-ee8a-42f7-bf04-fd0e00833ea9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 8d964a735d5c94775995d8c24ea0da25544c1ded
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552818"
---
# <a name="tutorial-azure-active-directory-integration-with-inkling"></a><span data-ttu-id="49f17-103">Tutorial: Azure Active Directory integration with Inkling</span><span class="sxs-lookup"><span data-stu-id="49f17-103">Tutorial: Azure Active Directory integration with Inkling</span></span>

<span data-ttu-id="49f17-104">In this tutorial, you learn how to integrate Inkling with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="49f17-104">In this tutorial, you learn how to integrate Inkling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="49f17-105">Integrating Inkling with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="49f17-105">Integrating Inkling with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="49f17-106">You can control in Azure AD who has access to Inkling</span><span class="sxs-lookup"><span data-stu-id="49f17-106">You can control in Azure AD who has access to Inkling</span></span>
- <span data-ttu-id="49f17-107">You can enable your users to automatically get signed-on to Inkling (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="49f17-107">You can enable your users to automatically get signed-on to Inkling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="49f17-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="49f17-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="49f17-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="49f17-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49f17-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="49f17-110">Prerequisites</span></span>

<span data-ttu-id="49f17-111">To configure Azure AD integration with Inkling, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="49f17-111">To configure Azure AD integration with Inkling, you need the following items:</span></span>

- <span data-ttu-id="49f17-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="49f17-112">An Azure AD subscription</span></span>
- <span data-ttu-id="49f17-113">An Inkling single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="49f17-113">An Inkling single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="49f17-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="49f17-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="49f17-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="49f17-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="49f17-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="49f17-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="49f17-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="49f17-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="49f17-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="49f17-118">Scenario description</span></span>
<span data-ttu-id="49f17-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="49f17-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="49f17-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="49f17-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="49f17-121">Adding Inkling from the gallery</span><span class="sxs-lookup"><span data-stu-id="49f17-121">Adding Inkling from the gallery</span></span>
2. <span data-ttu-id="49f17-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="49f17-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-inkling-from-the-gallery"></a><span data-ttu-id="49f17-123">Adding Inkling from the gallery</span><span class="sxs-lookup"><span data-stu-id="49f17-123">Adding Inkling from the gallery</span></span>
<span data-ttu-id="49f17-124">To configure the integration of Inkling into Azure AD, you need to add Inkling from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="49f17-124">To configure the integration of Inkling into Azure AD, you need to add Inkling from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="49f17-125">**To add Inkling from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="49f17-125">**To add Inkling from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="49f17-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="49f17-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="49f17-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="49f17-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="49f17-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="49f17-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="49f17-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="49f17-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="49f17-133">In the search box, type **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="49f17-133">In the search box, type **Inkling**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/tutorial_inkling_001.png)

5. <span data-ttu-id="49f17-135">In the results panel, select **Inkling**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="49f17-135">In the results panel, select **Inkling**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/tutorial_inkling_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="49f17-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="49f17-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="49f17-138">In this section, you configure and test Azure AD single sign-on with Inkling based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="49f17-138">In this section, you configure and test Azure AD single sign-on with Inkling based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="49f17-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Inkling is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49f17-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Inkling is to a user in Azure AD.</span></span> <span data-ttu-id="49f17-140">In other words, a link relationship between an Azure AD user and the related user in Inkling needs to be established.</span><span class="sxs-lookup"><span data-stu-id="49f17-140">In other words, a link relationship between an Azure AD user and the related user in Inkling needs to be established.</span></span>

<span data-ttu-id="49f17-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Inkling.</span><span class="sxs-lookup"><span data-stu-id="49f17-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Inkling.</span></span>

<span data-ttu-id="49f17-142">To configure and test Azure AD single sign-on with Inkling, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="49f17-142">To configure and test Azure AD single sign-on with Inkling, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="49f17-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="49f17-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="49f17-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="49f17-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="49f17-145">**[Creating an Inkling test user](#creating-an-inkling-test-user)** - to have a counterpart of Britta Simon in Inkling that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="49f17-145">**[Creating an Inkling test user](#creating-an-inkling-test-user)** - to have a counterpart of Britta Simon in Inkling that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="49f17-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="49f17-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="49f17-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="49f17-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="49f17-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="49f17-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="49f17-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Inkling application.</span><span class="sxs-lookup"><span data-stu-id="49f17-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Inkling application.</span></span>

<span data-ttu-id="49f17-150">**To configure Azure AD single sign-on with Inkling, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="49f17-150">**To configure Azure AD single sign-on with Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="49f17-151">In the Azure Management portal, on the **Inkling** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="49f17-151">In the Azure Management portal, on the **Inkling** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="49f17-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="49f17-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="49f17-155">On the **Inkling Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="49f17-155">On the **Inkling Domain and URLs** section, perform the following steps:</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/tutorial_inkling_01.png)

    <span data-ttu-id="49f17-157">a.</span><span class="sxs-lookup"><span data-stu-id="49f17-157">a.</span></span> <span data-ttu-id="49f17-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="49f17-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span></span>

    <span data-ttu-id="49f17-159">b.</span><span class="sxs-lookup"><span data-stu-id="49f17-159">b.</span></span> <span data-ttu-id="49f17-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/acs/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="49f17-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/acs/<user-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="49f17-161">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="49f17-161">Please note that these are not the real values.</span></span> <span data-ttu-id="49f17-162">You have to update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="49f17-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="49f17-163">Contact [Inkling support team](mailto:press@inkling.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="49f17-163">Contact [Inkling support team](mailto:press@inkling.com) to get these values.</span></span>

4. <span data-ttu-id="49f17-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="49f17-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/tutorial_general_400.png)   

5. <span data-ttu-id="49f17-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span><span class="sxs-lookup"><span data-stu-id="49f17-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="49f17-167">Then click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="49f17-167">Then click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="49f17-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="49f17-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/tutorial_inkling_02.png)

7. <span data-ttu-id="49f17-171">On the pop-up **Rollover certificate** window, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="49f17-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="49f17-173">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="49f17-173">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/tutorial_inkling_03.png) 

9. <span data-ttu-id="49f17-175">To get SSO configured for your application, contact [Inkling support team](mailto:press@inkling.com) and provide them with downloaded **metadata**.</span><span class="sxs-lookup"><span data-stu-id="49f17-175">To get SSO configured for your application, contact [Inkling support team](mailto:press@inkling.com) and provide them with downloaded **metadata**.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="49f17-176">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="49f17-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="49f17-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="49f17-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="49f17-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="49f17-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="49f17-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="49f17-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="49f17-182">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="49f17-182">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="49f17-184">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="49f17-184">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="49f17-186">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="49f17-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="49f17-188">a.</span><span class="sxs-lookup"><span data-stu-id="49f17-188">a.</span></span> <span data-ttu-id="49f17-189">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="49f17-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="49f17-190">b.</span><span class="sxs-lookup"><span data-stu-id="49f17-190">b.</span></span> <span data-ttu-id="49f17-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="49f17-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="49f17-192">c.</span><span class="sxs-lookup"><span data-stu-id="49f17-192">c.</span></span> <span data-ttu-id="49f17-193">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="49f17-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="49f17-194">d.</span><span class="sxs-lookup"><span data-stu-id="49f17-194">d.</span></span> <span data-ttu-id="49f17-195">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="49f17-195">Click **Create**.</span></span> 



### <a name="creating-an-inkling-test-user"></a><span data-ttu-id="49f17-196">Creating an Inkling test user</span><span class="sxs-lookup"><span data-stu-id="49f17-196">Creating an Inkling test user</span></span>

<span data-ttu-id="49f17-197">In this section, you create a user called Britta Simon in Inkling.</span><span class="sxs-lookup"><span data-stu-id="49f17-197">In this section, you create a user called Britta Simon in Inkling.</span></span> <span data-ttu-id="49f17-198">Please work with [Inkling support team](mailto:press@inkling.com) to add the users in the Inkling platform.</span><span class="sxs-lookup"><span data-stu-id="49f17-198">Please work with [Inkling support team](mailto:press@inkling.com) to add the users in the Inkling platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="49f17-199">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="49f17-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="49f17-200">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Inkling.</span><span class="sxs-lookup"><span data-stu-id="49f17-200">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Inkling.</span></span>

![Assign User][200] 

<span data-ttu-id="49f17-202">**To assign Britta Simon to Inkling, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="49f17-202">**To assign Britta Simon to Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="49f17-203">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="49f17-203">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="49f17-205">In the applications list, select **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="49f17-205">In the applications list, select **Inkling**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/tutorial_inkling_50.png) 

3. <span data-ttu-id="49f17-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="49f17-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="49f17-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="49f17-209">Click **Add** button.</span></span> <span data-ttu-id="49f17-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="49f17-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="49f17-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="49f17-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="49f17-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="49f17-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="49f17-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="49f17-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="49f17-215">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="49f17-215">Testing single sign-on</span></span>

<span data-ttu-id="49f17-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="49f17-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="49f17-217">When you click the Inkling tile in the Access Panel, you should get automatically signed-on to your Inkling application.</span><span class="sxs-lookup"><span data-stu-id="49f17-217">When you click the Inkling tile in the Access Panel, you should get automatically signed-on to your Inkling application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="49f17-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="49f17-218">Additional resources</span></span>

* [<span data-ttu-id="49f17-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49f17-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="49f17-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="49f17-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-inkling-tutorial/tutorial_general_203.png






















