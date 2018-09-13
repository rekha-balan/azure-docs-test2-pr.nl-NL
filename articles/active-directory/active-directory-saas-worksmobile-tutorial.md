---
title: 'Tutorial: Azure Active Directory integration with WORKS MOBILE | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and WORKS MOBILE.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: jeedes
ms.openlocfilehash: 2ec4e0838a96351a9bddd9c5affd21b5c55f72c8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564310"
---
# <a name="tutorial-azure-active-directory-integration-with-works-mobile"></a><span data-ttu-id="df8fe-103">Tutorial: Azure Active Directory integration with WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="df8fe-103">Tutorial: Azure Active Directory integration with WORKS MOBILE</span></span>

<span data-ttu-id="df8fe-104">In this tutorial, you learn how to integrate WORKS MOBILE with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="df8fe-104">In this tutorial, you learn how to integrate WORKS MOBILE with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="df8fe-105">Integrating WORKS MOBILE with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="df8fe-105">Integrating WORKS MOBILE with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="df8fe-106">You can control in Azure AD who has access to WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="df8fe-106">You can control in Azure AD who has access to WORKS MOBILE</span></span>
- <span data-ttu-id="df8fe-107">You can enable your users to automatically get signed-on to WORKS MOBILE single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="df8fe-107">You can enable your users to automatically get signed-on to WORKS MOBILE single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="df8fe-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="df8fe-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="df8fe-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="df8fe-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df8fe-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="df8fe-110">Prerequisites</span></span>

<span data-ttu-id="df8fe-111">To configure Azure AD integration with WORKS MOBILE, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="df8fe-111">To configure Azure AD integration with WORKS MOBILE, you need the following items:</span></span>

- <span data-ttu-id="df8fe-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="df8fe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="df8fe-113">A WORKS MOBILE SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="df8fe-113">A WORKS MOBILE SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="df8fe-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="df8fe-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="df8fe-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="df8fe-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="df8fe-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="df8fe-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="df8fe-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="df8fe-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="df8fe-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="df8fe-118">Scenario description</span></span>
<span data-ttu-id="df8fe-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="df8fe-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="df8fe-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="df8fe-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="df8fe-121">Adding WORKS MOBILE from the gallery</span><span class="sxs-lookup"><span data-stu-id="df8fe-121">Adding WORKS MOBILE from the gallery</span></span>
2. <span data-ttu-id="df8fe-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="df8fe-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-works-mobile-from-the-gallery"></a><span data-ttu-id="df8fe-123">Add WORKS MOBILE from the gallery</span><span class="sxs-lookup"><span data-stu-id="df8fe-123">Add WORKS MOBILE from the gallery</span></span>
<span data-ttu-id="df8fe-124">To configure the integration of WORKS MOBILE into Azure AD, you need to add WORKS MOBILE from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="df8fe-124">To configure the integration of WORKS MOBILE into Azure AD, you need to add WORKS MOBILE from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="df8fe-125">**To add WORKS MOBILE from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="df8fe-125">**To add WORKS MOBILE from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="df8fe-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="df8fe-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]
2. <span data-ttu-id="df8fe-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="df8fe-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="df8fe-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="df8fe-129">Then go to **All applications**.</span></span>

    ![Applications][2]
3. <span data-ttu-id="df8fe-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="df8fe-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]
4. <span data-ttu-id="df8fe-133">In the search box, type **WORKS MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="df8fe-133">In the search box, type **WORKS MOBILE**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_001.png)

5. <span data-ttu-id="df8fe-135">In the results panel, select **WORKS MOBILE**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="df8fe-135">In the results panel, select **WORKS MOBILE**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_0001.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="df8fe-137">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="df8fe-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="df8fe-138">In this section, you configure and test Azure AD SSO with WORKS MOBILE based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="df8fe-138">In this section, you configure and test Azure AD SSO with WORKS MOBILE based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="df8fe-139">For SSO to work, Azure AD needs to know what the counterpart user in WORKS MOBILE is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df8fe-139">For SSO to work, Azure AD needs to know what the counterpart user in WORKS MOBILE is to a user in Azure AD.</span></span> <span data-ttu-id="df8fe-140">In other words, a link relationship between an Azure AD user and the related user in WORKS MOBILE needs to be established.</span><span class="sxs-lookup"><span data-stu-id="df8fe-140">In other words, a link relationship between an Azure AD user and the related user in WORKS MOBILE needs to be established.</span></span>

<span data-ttu-id="df8fe-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="df8fe-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in WORKS MOBILE.</span></span>

<span data-ttu-id="df8fe-142">To configure and test Azure AD SSO with WORKS MOBILE, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="df8fe-142">To configure and test Azure AD SSO with WORKS MOBILE, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="df8fe-143">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="df8fe-143">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="df8fe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df8fe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="df8fe-145">**[Creating a WORKS MOBILE test user](#creating-a-works-mobile-test-user)** - to have a counterpart of Britta Simon in WORKS MOBILE that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="df8fe-145">**[Creating a WORKS MOBILE test user](#creating-a-works-mobile-test-user)** - to have a counterpart of Britta Simon in WORKS MOBILE that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="df8fe-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="df8fe-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="df8fe-147">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="df8fe-147">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="df8fe-148">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="df8fe-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="df8fe-149">In this section, you enable Azure AD SSO in the Azure Management portal and configure SSO in your WORKS MOBILE application.</span><span class="sxs-lookup"><span data-stu-id="df8fe-149">In this section, you enable Azure AD SSO in the Azure Management portal and configure SSO in your WORKS MOBILE application.</span></span>

<span data-ttu-id="df8fe-150">**To configure Azure AD SSO with WORKS MOBILE, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="df8fe-150">**To configure Azure AD SSO with WORKS MOBILE, perform the following steps:**</span></span>

1. <span data-ttu-id="df8fe-151">In the Azure Management portal, on the **WORKS MOBILE** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="df8fe-151">In the Azure Management portal, on the **WORKS MOBILE** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]
2. <span data-ttu-id="df8fe-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="df8fe-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_01.png)
3. <span data-ttu-id="df8fe-155">On the **WORKS MOBILE Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="df8fe-155">On the **WORKS MOBILE Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_02.png)
  1. <span data-ttu-id="df8fe-157">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.worksmobile.com/jp/myservice`</span><span class="sxs-lookup"><span data-stu-id="df8fe-157">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.worksmobile.com/jp/myservice`</span></span>
  2. <span data-ttu-id="df8fe-158">In the **Identifier** textbox, type the value as `worksmobile.com`</span><span class="sxs-lookup"><span data-stu-id="df8fe-158">In the **Identifier** textbox, type the value as `worksmobile.com`</span></span>

    >[!NOTE] 
    ><span data-ttu-id="df8fe-159">These are not the real values.</span><span class="sxs-lookup"><span data-stu-id="df8fe-159">These are not the real values.</span></span> <span data-ttu-id="df8fe-160">You have to update these values with the actual Sign On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="df8fe-160">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="df8fe-161">Here we suggest you to use the unique value of string in the Identifier.</span><span class="sxs-lookup"><span data-stu-id="df8fe-161">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="df8fe-162">Contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="df8fe-162">Contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) to get these values.</span></span> 
    >
    >

4. <span data-ttu-id="df8fe-163">On the **SAML Signing Certificate** section, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="df8fe-163">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_03.png)    
5. <span data-ttu-id="df8fe-165">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span><span class="sxs-lookup"><span data-stu-id="df8fe-165">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="df8fe-166">Then click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="df8fe-166">Then click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_general_300.png)
6. <span data-ttu-id="df8fe-168">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="df8fe-168">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_04.png)
7. <span data-ttu-id="df8fe-170">On the pop-up **Rollover certificate** window, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="df8fe-170">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_general_400.png)
8. <span data-ttu-id="df8fe-172">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="df8fe-172">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_05.png) 

9. <span data-ttu-id="df8fe-174">On the **WORKS MOBILE Configuration** section, click **Configure WORKS MOBILE** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="df8fe-174">On the **WORKS MOBILE Configuration** section, click **Configure WORKS MOBILE** to open **Configure sign-on** window.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_06.png) 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_07.png)

10. <span data-ttu-id="df8fe-177">To get SSO configured for your application, contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) and provide them with the following: •  The downloaded **Certificate file** •  The **SAML Single Sign-On Service URL** •  The **SAML Entity ID** •  The **Sign-Out URL**</span><span class="sxs-lookup"><span data-stu-id="df8fe-177">To get SSO configured for your application, contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) and provide them with the following: •  The downloaded **Certificate file** •  The **SAML Single Sign-On Service URL** •  The **SAML Entity ID** •  The **Sign-Out URL**</span></span>
  
### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="df8fe-178">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="df8fe-178">Create an Azure AD test user</span></span>
<span data-ttu-id="df8fe-179">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df8fe-179">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="df8fe-181">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="df8fe-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="df8fe-182">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="df8fe-182">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/create_aaduser_01.png) 
2. <span data-ttu-id="df8fe-184">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="df8fe-184">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/create_aaduser_02.png) 
3. <span data-ttu-id="df8fe-186">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="df8fe-186">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="df8fe-188">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="df8fe-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="df8fe-190">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="df8fe-190">In the **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="df8fe-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="df8fe-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="df8fe-192">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="df8fe-192">Select **Show Password** and write down the value of the **Password**.</span></span>
  4. <span data-ttu-id="df8fe-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="df8fe-193">Click **Create**.</span></span> 

### <a name="create-a-works-mobile-test-user"></a><span data-ttu-id="df8fe-194">Create a WORKS MOBILE test user</span><span class="sxs-lookup"><span data-stu-id="df8fe-194">Create a WORKS MOBILE test user</span></span>

<span data-ttu-id="df8fe-195">In this section, you create a user called Britta Simon in WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="df8fe-195">In this section, you create a user called Britta Simon in WORKS MOBILE.</span></span> <span data-ttu-id="df8fe-196">Please work with [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) to add the users in the WORKS MOBILE platform.</span><span class="sxs-lookup"><span data-stu-id="df8fe-196">Please work with [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) to add the users in the WORKS MOBILE platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="df8fe-197">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="df8fe-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="df8fe-198">In this section, you enable Britta Simon to use Azure SSO by granting her access to WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="df8fe-198">In this section, you enable Britta Simon to use Azure SSO by granting her access to WORKS MOBILE.</span></span>

![Assign User][200] 

<span data-ttu-id="df8fe-200">**To assign Britta Simon to WORKS MOBILE, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="df8fe-200">**To assign Britta Simon to WORKS MOBILE, perform the following steps:**</span></span>

1. <span data-ttu-id="df8fe-201">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="df8fe-201">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="df8fe-203">In the applications list, select **WORKS MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="df8fe-203">In the applications list, select **WORKS MOBILE**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_50.png) 

3. <span data-ttu-id="df8fe-205">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="df8fe-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="df8fe-207">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="df8fe-207">Click **Add** button.</span></span> <span data-ttu-id="df8fe-208">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="df8fe-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="df8fe-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="df8fe-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>
6. <span data-ttu-id="df8fe-211">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="df8fe-211">Click **Select** button on **Users and groups** dialog.</span></span>
7. <span data-ttu-id="df8fe-212">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="df8fe-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="df8fe-213">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="df8fe-213">Test single sign-on</span></span>

<span data-ttu-id="df8fe-214">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="df8fe-214">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="df8fe-215">When you click the WORKS MOBILE tile in the Access Panel, you should get automatically signed-on to your WORKS MOBILE application.</span><span class="sxs-lookup"><span data-stu-id="df8fe-215">When you click the WORKS MOBILE tile in the Access Panel, you should get automatically signed-on to your WORKS MOBILE application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="df8fe-216">Additional resources</span><span class="sxs-lookup"><span data-stu-id="df8fe-216">Additional resources</span></span>

* [<span data-ttu-id="df8fe-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="df8fe-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="df8fe-218">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="df8fe-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-worksmobile-tutorial/tutorial_general_203.png
























