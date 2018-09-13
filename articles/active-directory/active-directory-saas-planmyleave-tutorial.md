---
title: 'Tutorial: Azure Active Directory integration with PlanMyLeave | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and PlanMyLeave.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: 919c3c9d75f67f817f96a5cbe0d1bef7b2cf5409
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551075"
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="ce473-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="ce473-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="ce473-104">In this tutorial, you learn how to integrate PlanMyLeave with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ce473-104">In this tutorial, you learn how to integrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ce473-105">Integrating PlanMyLeave with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ce473-105">Integrating PlanMyLeave with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ce473-106">You can control in Azure AD who has access to PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="ce473-106">You can control in Azure AD who has access to PlanMyLeave</span></span>
- <span data-ttu-id="ce473-107">You can enable your users to automatically get signed-on to PlanMyLeave (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="ce473-107">You can enable your users to automatically get signed-on to PlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ce473-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="ce473-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="ce473-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ce473-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce473-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ce473-110">Prerequisites</span></span>

<span data-ttu-id="ce473-111">To configure Azure AD integration with PlanMyLeave, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ce473-111">To configure Azure AD integration with PlanMyLeave, you need the following items:</span></span>

- <span data-ttu-id="ce473-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ce473-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ce473-113">A PlanMyLeave single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ce473-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="ce473-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ce473-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="ce473-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ce473-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ce473-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="ce473-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ce473-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ce473-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="ce473-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="ce473-118">Scenario description</span></span>
<span data-ttu-id="ce473-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ce473-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ce473-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ce473-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ce473-121">Adding PlanMyLeave from the gallery</span><span class="sxs-lookup"><span data-stu-id="ce473-121">Adding PlanMyLeave from the gallery</span></span>
2. <span data-ttu-id="ce473-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ce473-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-the-gallery"></a><span data-ttu-id="ce473-123">Adding PlanMyLeave from the gallery</span><span class="sxs-lookup"><span data-stu-id="ce473-123">Adding PlanMyLeave from the gallery</span></span>
<span data-ttu-id="ce473-124">To configure the integration of PlanMyLeave into Azure AD, you need to add PlanMyLeave from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ce473-124">To configure the integration of PlanMyLeave into Azure AD, you need to add PlanMyLeave from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ce473-125">**To add PlanMyLeave from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ce473-125">**To add PlanMyLeave from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ce473-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ce473-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ce473-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="ce473-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ce473-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ce473-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="ce473-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="ce473-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ce473-133">In the search box, type **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="ce473-133">In the search box, type **PlanMyLeave**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="ce473-135">In the results panel, select **PlanMyLeave**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="ce473-135">In the results panel, select **PlanMyLeave**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ce473-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ce473-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ce473-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ce473-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ce473-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PlanMyLeave is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce473-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PlanMyLeave is to a user in Azure AD.</span></span> <span data-ttu-id="ce473-140">In other words, a link relationship between an Azure AD user and the related user in PlanMyLeave needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ce473-140">In other words, a link relationship between an Azure AD user and the related user in PlanMyLeave needs to be established.</span></span>

<span data-ttu-id="ce473-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="ce473-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="ce473-142">To configure and test Azure AD single sign-on with PlanMyLeave, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ce473-142">To configure and test Azure AD single sign-on with PlanMyLeave, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ce473-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ce473-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ce473-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ce473-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ce473-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - to have a counterpart of Britta Simon in PlanMyLeave that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="ce473-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - to have a counterpart of Britta Simon in PlanMyLeave that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="ce473-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ce473-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ce473-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ce473-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ce473-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ce473-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ce473-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your PlanMyLeave application.</span><span class="sxs-lookup"><span data-stu-id="ce473-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="ce473-150">**To configure Azure AD single sign-on with PlanMyLeave, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ce473-150">**To configure Azure AD single sign-on with PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="ce473-151">In the Azure Management portal, on the **PlanMyLeave** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ce473-151">In the Azure Management portal, on the **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="ce473-153">On the **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="ce473-153">On the **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="ce473-155">On the **PlanMyLeave Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ce473-155">On the **PlanMyLeave Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="ce473-157">a.</span><span class="sxs-lookup"><span data-stu-id="ce473-157">a.</span></span> <span data-ttu-id="ce473-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="ce473-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="ce473-159">b.</span><span class="sxs-lookup"><span data-stu-id="ce473-159">b.</span></span> <span data-ttu-id="ce473-160">In the **Identifer** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com`</span><span class="sxs-lookup"><span data-stu-id="ce473-160">In the **Identifer** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ce473-161">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="ce473-161">Please note that these are not the real values.</span></span> <span data-ttu-id="ce473-162">You have to update these values with the actual Sign On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="ce473-162">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="ce473-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="ce473-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) to get these values.</span></span>

4. <span data-ttu-id="ce473-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="ce473-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)    

5. <span data-ttu-id="ce473-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span><span class="sxs-lookup"><span data-stu-id="ce473-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="ce473-167">Then click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="ce473-167">Then click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="ce473-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="ce473-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="ce473-171">On the pop-up **Rollover certificate** window, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ce473-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ce473-173">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ce473-173">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="ce473-175">On the **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="ce473-175">On the **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** to open **Configure sign-on** window.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="ce473-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ce473-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="ce473-179">Go to **System Setup**.</span><span class="sxs-lookup"><span data-stu-id="ce473-179">Go to **System Setup**.</span></span> <span data-ttu-id="ce473-180">Then on the **Security Management** section click **Company SAML settings** .</span><span class="sxs-lookup"><span data-stu-id="ce473-180">Then on the **Security Management** section click **Company SAML settings** .</span></span>

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="ce473-182">On the **SAML Settings** section, click editor icon.</span><span class="sxs-lookup"><span data-stu-id="ce473-182">On the **SAML Settings** section, click editor icon.</span></span>

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="ce473-184">On the **Update SAML Settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ce473-184">On the **Update SAML Settings** section, perform the following steps:</span></span>

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="ce473-186">a.</span><span class="sxs-lookup"><span data-stu-id="ce473-186">a.</span></span>  <span data-ttu-id="ce473-187">In the **Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="ce473-187">In the **Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="ce473-188">b.</span><span class="sxs-lookup"><span data-stu-id="ce473-188">b.</span></span>  <span data-ttu-id="ce473-189">Open your downloaded certificate file in notepad, copy only the content between the ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it to the **Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="ce473-189">Open your downloaded certificate file in notepad, copy only the content between the ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>

    <span data-ttu-id="ce473-190">c.</span><span class="sxs-lookup"><span data-stu-id="ce473-190">c.</span></span> <span data-ttu-id="ce473-191">Set "**Is Enable**" to "**Yes**".</span><span class="sxs-lookup"><span data-stu-id="ce473-191">Set "**Is Enable**" to "**Yes**".</span></span>

    <span data-ttu-id="ce473-192">d.</span><span class="sxs-lookup"><span data-stu-id="ce473-192">d.</span></span> <span data-ttu-id="ce473-193">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ce473-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ce473-194">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ce473-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="ce473-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ce473-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="ce473-197">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ce473-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ce473-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ce473-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ce473-200">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="ce473-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ce473-202">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="ce473-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ce473-204">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ce473-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ce473-206">a.</span><span class="sxs-lookup"><span data-stu-id="ce473-206">a.</span></span> <span data-ttu-id="ce473-207">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ce473-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ce473-208">b.</span><span class="sxs-lookup"><span data-stu-id="ce473-208">b.</span></span> <span data-ttu-id="ce473-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ce473-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ce473-210">c.</span><span class="sxs-lookup"><span data-stu-id="ce473-210">c.</span></span> <span data-ttu-id="ce473-211">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="ce473-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ce473-212">d.</span><span class="sxs-lookup"><span data-stu-id="ce473-212">d.</span></span> <span data-ttu-id="ce473-213">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ce473-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="ce473-214">Creating a PlanMyLeave test user</span><span class="sxs-lookup"><span data-stu-id="ce473-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="ce473-215">The objective of this section is to create a user called Britta Simon in PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="ce473-215">The objective of this section is to create a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="ce473-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="ce473-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="ce473-217">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="ce473-217">There is no action item for you in this section.</span></span> <span data-ttu-id="ce473-218">A new user will be created during an attempt to access PlanMyLeave if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="ce473-218">A new user will be created during an attempt to access PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="ce473-219">If you need to create an user manually, you need to contact [PlanMyLeave support team](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="ce473-219">If you need to create an user manually, you need to contact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ce473-220">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ce473-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ce473-221">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="ce473-221">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to PlanMyLeave.</span></span>

![Assign User][200] 

<span data-ttu-id="ce473-223">**To assign Britta Simon to PlanMyLeave, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ce473-223">**To assign Britta Simon to PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="ce473-224">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ce473-224">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="ce473-226">In the applications list, select **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="ce473-226">In the applications list, select **PlanMyLeave**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="ce473-228">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="ce473-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="ce473-230">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="ce473-230">Click **Add** button.</span></span> <span data-ttu-id="ce473-231">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ce473-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="ce473-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="ce473-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ce473-234">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="ce473-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ce473-235">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ce473-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="ce473-236">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="ce473-236">Testing single sign-on</span></span>

<span data-ttu-id="ce473-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ce473-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ce473-238">When you click the PlanMyLeave tile in the Access Panel, you should get automatically signed-on to your PlanMyLeave application.</span><span class="sxs-lookup"><span data-stu-id="ce473-238">When you click the PlanMyLeave tile in the Access Panel, you should get automatically signed-on to your PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="ce473-239">Additional resources</span><span class="sxs-lookup"><span data-stu-id="ce473-239">Additional resources</span></span>

* [<span data-ttu-id="ce473-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ce473-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ce473-241">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ce473-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png



























