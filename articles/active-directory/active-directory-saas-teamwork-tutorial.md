---
title: 'Tutorial: Azure Active Directory integration with Teamwork | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Teamwork.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03760032-3d76-4b47-ab84-241f72fbd561
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 8d24759e1cfb6c12a5c705eb1316e11bf4253a28
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550101"
---
# <a name="tutorial-azure-active-directory-integration-with-teamwork"></a><span data-ttu-id="da9c8-103">Tutorial: Azure Active Directory integration with Teamwork</span><span class="sxs-lookup"><span data-stu-id="da9c8-103">Tutorial: Azure Active Directory integration with Teamwork</span></span>

<span data-ttu-id="da9c8-104">In this tutorial, you learn how to integrate Teamwork with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="da9c8-104">In this tutorial, you learn how to integrate Teamwork with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="da9c8-105">Integrating Teamwork with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="da9c8-105">Integrating Teamwork with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="da9c8-106">You can control in Azure AD who has access to Teamwork</span><span class="sxs-lookup"><span data-stu-id="da9c8-106">You can control in Azure AD who has access to Teamwork</span></span>
- <span data-ttu-id="da9c8-107">You can enable your users to automatically get signed-on to Teamwork (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="da9c8-107">You can enable your users to automatically get signed-on to Teamwork (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="da9c8-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="da9c8-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="da9c8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="da9c8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da9c8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="da9c8-110">Prerequisites</span></span>

<span data-ttu-id="da9c8-111">To configure Azure AD integration with Teamwork, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="da9c8-111">To configure Azure AD integration with Teamwork, you need the following items:</span></span>

- <span data-ttu-id="da9c8-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="da9c8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="da9c8-113">A Teamwork single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="da9c8-113">A Teamwork single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="da9c8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="da9c8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="da9c8-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="da9c8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="da9c8-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="da9c8-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="da9c8-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="da9c8-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="da9c8-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="da9c8-118">Scenario description</span></span>
<span data-ttu-id="da9c8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="da9c8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="da9c8-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="da9c8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="da9c8-121">Adding Teamwork from the gallery</span><span class="sxs-lookup"><span data-stu-id="da9c8-121">Adding Teamwork from the gallery</span></span>
2. <span data-ttu-id="da9c8-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="da9c8-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-teamwork-from-the-gallery"></a><span data-ttu-id="da9c8-123">Adding Teamwork from the gallery</span><span class="sxs-lookup"><span data-stu-id="da9c8-123">Adding Teamwork from the gallery</span></span>
<span data-ttu-id="da9c8-124">To configure the integration of Teamwork into Azure AD, you need to add Teamwork from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="da9c8-124">To configure the integration of Teamwork into Azure AD, you need to add Teamwork from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="da9c8-125">**To add Teamwork from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="da9c8-125">**To add Teamwork from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="da9c8-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="da9c8-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="da9c8-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="da9c8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="da9c8-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="da9c8-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="da9c8-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="da9c8-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="da9c8-133">In the search box, type **Teamwork**.</span><span class="sxs-lookup"><span data-stu-id="da9c8-133">In the search box, type **Teamwork**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_001.png)

5. <span data-ttu-id="da9c8-135">In the results panel, select **Teamwork**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="da9c8-135">In the results panel, select **Teamwork**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="da9c8-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="da9c8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="da9c8-138">In this section, you configure and test Azure AD single sign-on with Teamwork based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="da9c8-138">In this section, you configure and test Azure AD single sign-on with Teamwork based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="da9c8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamwork is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da9c8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamwork is to a user in Azure AD.</span></span> <span data-ttu-id="da9c8-140">In other words, a link relationship between an Azure AD user and the related user in Teamwork needs to be established.</span><span class="sxs-lookup"><span data-stu-id="da9c8-140">In other words, a link relationship between an Azure AD user and the related user in Teamwork needs to be established.</span></span>

<span data-ttu-id="da9c8-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamwork.</span><span class="sxs-lookup"><span data-stu-id="da9c8-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamwork.</span></span>

<span data-ttu-id="da9c8-142">To configure and test Azure AD single sign-on with Teamwork, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="da9c8-142">To configure and test Azure AD single sign-on with Teamwork, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="da9c8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="da9c8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="da9c8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="da9c8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="da9c8-145">**[Creating a Teamwork test user](#creating-a-teamwork-test-user)** - to have a counterpart of Britta Simon in Teamwork that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="da9c8-145">**[Creating a Teamwork test user](#creating-a-teamwork-test-user)** - to have a counterpart of Britta Simon in Teamwork that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="da9c8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="da9c8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="da9c8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="da9c8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="da9c8-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="da9c8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="da9c8-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamwork application.</span><span class="sxs-lookup"><span data-stu-id="da9c8-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamwork application.</span></span>

<span data-ttu-id="da9c8-150">**To configure Azure AD single sign-on with Teamwork, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="da9c8-150">**To configure Azure AD single sign-on with Teamwork, perform the following steps:**</span></span>

1. <span data-ttu-id="da9c8-151">In the Azure Management portal, on the **Teamwork** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="da9c8-151">In the Azure Management portal, on the **Teamwork** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="da9c8-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="da9c8-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_01.png)

3. <span data-ttu-id="da9c8-155">On the **Teamwork Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.teamwork.com`</span><span class="sxs-lookup"><span data-stu-id="da9c8-155">On the **Teamwork Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.teamwork.com`</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_02.png)

    > [!NOTE] 
    > <span data-ttu-id="da9c8-157">Please note that this is not the real value.</span><span class="sxs-lookup"><span data-stu-id="da9c8-157">Please note that this is not the real value.</span></span> <span data-ttu-id="da9c8-158">You have to update this value with the actual Sign On URL.</span><span class="sxs-lookup"><span data-stu-id="da9c8-158">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="da9c8-159">Contact [Teamwork support team](mailto:support@teamwork.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="da9c8-159">Contact [Teamwork support team](mailto:support@teamwork.com) to get this value.</span></span> 

4. <span data-ttu-id="da9c8-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="da9c8-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_03.png)  

5. <span data-ttu-id="da9c8-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span><span class="sxs-lookup"><span data-stu-id="da9c8-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="da9c8-163">Then click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="da9c8-163">Then click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="da9c8-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="da9c8-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_04.png)

7. <span data-ttu-id="da9c8-167">On the pop-up **Rollover certificate** window, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="da9c8-167">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="da9c8-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="da9c8-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_05.png) 

9. <span data-ttu-id="da9c8-171">To get SSO configured for your application, contact [Teamwork support team](mailto:support@teamwork.com) and provide them with the downloaded **metadata**.</span><span class="sxs-lookup"><span data-stu-id="da9c8-171">To get SSO configured for your application, contact [Teamwork support team](mailto:support@teamwork.com) and provide them with the downloaded **metadata**.</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="da9c8-172">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="da9c8-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="da9c8-173">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="da9c8-173">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="da9c8-175">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="da9c8-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="da9c8-176">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="da9c8-176">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="da9c8-178">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="da9c8-178">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="da9c8-180">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="da9c8-180">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="da9c8-182">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="da9c8-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="da9c8-184">a.</span><span class="sxs-lookup"><span data-stu-id="da9c8-184">a.</span></span> <span data-ttu-id="da9c8-185">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="da9c8-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="da9c8-186">b.</span><span class="sxs-lookup"><span data-stu-id="da9c8-186">b.</span></span> <span data-ttu-id="da9c8-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="da9c8-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="da9c8-188">c.</span><span class="sxs-lookup"><span data-stu-id="da9c8-188">c.</span></span> <span data-ttu-id="da9c8-189">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="da9c8-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="da9c8-190">d.</span><span class="sxs-lookup"><span data-stu-id="da9c8-190">d.</span></span> <span data-ttu-id="da9c8-191">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="da9c8-191">Click **Create**.</span></span> 



### <a name="creating-a-teamwork-test-user"></a><span data-ttu-id="da9c8-192">Creating a Teamwork test user</span><span class="sxs-lookup"><span data-stu-id="da9c8-192">Creating a Teamwork test user</span></span>

<span data-ttu-id="da9c8-193">In this section, you create a user called Britta Simon in Teamwork.</span><span class="sxs-lookup"><span data-stu-id="da9c8-193">In this section, you create a user called Britta Simon in Teamwork.</span></span> <span data-ttu-id="da9c8-194">Please work with [Teamwork support team](mailto:support@teamwork.com) to add the users in the Teamwork platform.</span><span class="sxs-lookup"><span data-stu-id="da9c8-194">Please work with [Teamwork support team](mailto:support@teamwork.com) to add the users in the Teamwork platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="da9c8-195">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="da9c8-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="da9c8-196">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamwork.</span><span class="sxs-lookup"><span data-stu-id="da9c8-196">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamwork.</span></span>

![Assign User][200] 

<span data-ttu-id="da9c8-198">**To assign Britta Simon to Teamwork, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="da9c8-198">**To assign Britta Simon to Teamwork, perform the following steps:**</span></span>

1. <span data-ttu-id="da9c8-199">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="da9c8-199">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="da9c8-201">In the applications list, select **Teamwork**.</span><span class="sxs-lookup"><span data-stu-id="da9c8-201">In the applications list, select **Teamwork**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_50.png) 

3. <span data-ttu-id="da9c8-203">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="da9c8-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="da9c8-205">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="da9c8-205">Click **Add** button.</span></span> <span data-ttu-id="da9c8-206">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="da9c8-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="da9c8-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="da9c8-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="da9c8-209">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="da9c8-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="da9c8-210">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="da9c8-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="da9c8-211">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="da9c8-211">Testing single sign-on</span></span>

<span data-ttu-id="da9c8-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="da9c8-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="da9c8-213">When you click the Teamwork tile in the Access Panel, you should get automatically signed-on to your Teamwork application.</span><span class="sxs-lookup"><span data-stu-id="da9c8-213">When you click the Teamwork tile in the Access Panel, you should get automatically signed-on to your Teamwork application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="da9c8-214">Additional resources</span><span class="sxs-lookup"><span data-stu-id="da9c8-214">Additional resources</span></span>

* [<span data-ttu-id="da9c8-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="da9c8-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="da9c8-216">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="da9c8-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-teamwork-tutorial/tutorial_general_203.png






















