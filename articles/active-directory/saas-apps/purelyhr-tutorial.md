---
title: 'Tutorial: Azure Active Directory integration with PurelyHR | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and PurelyHR.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 86a9c454-596d-4902-829a-fe126708f739
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: c02dc274c5d22c16b2bda6d7896ee64c41d6e2ab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864335"
---
# <a name="tutorial-azure-active-directory-integration-with-purelyhr"></a><span data-ttu-id="d0f58-103">Tutorial: Azure Active Directory integration with PurelyHR</span><span class="sxs-lookup"><span data-stu-id="d0f58-103">Tutorial: Azure Active Directory integration with PurelyHR</span></span>

<span data-ttu-id="d0f58-104">In this tutorial, you learn how to integrate PurelyHR with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d0f58-104">In this tutorial, you learn how to integrate PurelyHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d0f58-105">Integrating PurelyHR with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d0f58-105">Integrating PurelyHR with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d0f58-106">You can control in Azure AD who has access to PurelyHR</span><span class="sxs-lookup"><span data-stu-id="d0f58-106">You can control in Azure AD who has access to PurelyHR</span></span>
- <span data-ttu-id="d0f58-107">You can enable your users to automatically get signed-on to PurelyHR (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="d0f58-107">You can enable your users to automatically get signed-on to PurelyHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d0f58-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d0f58-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d0f58-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="d0f58-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0f58-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d0f58-110">Prerequisites</span></span>

<span data-ttu-id="d0f58-111">To configure Azure AD integration with PurelyHR, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d0f58-111">To configure Azure AD integration with PurelyHR, you need the following items:</span></span>

- <span data-ttu-id="d0f58-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d0f58-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d0f58-113">A PurelyHR single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d0f58-113">A PurelyHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d0f58-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d0f58-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d0f58-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d0f58-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d0f58-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="d0f58-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d0f58-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0f58-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d0f58-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="d0f58-118">Scenario description</span></span>
<span data-ttu-id="d0f58-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d0f58-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d0f58-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d0f58-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d0f58-121">Adding PurelyHR from the gallery</span><span class="sxs-lookup"><span data-stu-id="d0f58-121">Adding PurelyHR from the gallery</span></span>
1. <span data-ttu-id="d0f58-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d0f58-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-purelyhr-from-the-gallery"></a><span data-ttu-id="d0f58-123">Adding PurelyHR from the gallery</span><span class="sxs-lookup"><span data-stu-id="d0f58-123">Adding PurelyHR from the gallery</span></span>
<span data-ttu-id="d0f58-124">To configure the integration of PurelyHR into Azure AD, you need to add PurelyHR from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d0f58-124">To configure the integration of PurelyHR into Azure AD, you need to add PurelyHR from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d0f58-125">**To add PurelyHR from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d0f58-125">**To add PurelyHR from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d0f58-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d0f58-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="d0f58-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="d0f58-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d0f58-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d0f58-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="d0f58-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="d0f58-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="d0f58-133">In the search box, type **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="d0f58-133">In the search box, type **PurelyHR**.</span></span>

    ![Creating an Azure AD test user](./media/purelyhr-tutorial/tutorial_purelyhr_search.png)

1. <span data-ttu-id="d0f58-135">In the results panel, select **PurelyHR**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="d0f58-135">In the results panel, select **PurelyHR**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/purelyhr-tutorial/tutorial_purelyhr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d0f58-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d0f58-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d0f58-138">In this section, you configure and test Azure AD single sign-on with PurelyHR based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="d0f58-138">In this section, you configure and test Azure AD single sign-on with PurelyHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d0f58-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PurelyHR is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0f58-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PurelyHR is to a user in Azure AD.</span></span> <span data-ttu-id="d0f58-140">In other words, a link relationship between an Azure AD user and the related user in PurelyHR needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d0f58-140">In other words, a link relationship between an Azure AD user and the related user in PurelyHR needs to be established.</span></span>

<span data-ttu-id="d0f58-141">In PurelyHR, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="d0f58-141">In PurelyHR, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d0f58-142">To configure and test Azure AD single sign-on with PurelyHR, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d0f58-142">To configure and test Azure AD single sign-on with PurelyHR, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d0f58-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d0f58-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="d0f58-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d0f58-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="d0f58-145">**[Creating a PurelyHR test user](#creating-a-purelyhr-test-user)** - to have a counterpart of Britta Simon in PurelyHR that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="d0f58-145">**[Creating a PurelyHR test user](#creating-a-purelyhr-test-user)** - to have a counterpart of Britta Simon in PurelyHR that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="d0f58-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d0f58-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="d0f58-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d0f58-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d0f58-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d0f58-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d0f58-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PurelyHR application.</span><span class="sxs-lookup"><span data-stu-id="d0f58-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PurelyHR application.</span></span>

<span data-ttu-id="d0f58-150">**To configure Azure AD single sign-on with PurelyHR, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d0f58-150">**To configure Azure AD single sign-on with PurelyHR, perform the following steps:**</span></span>

1. <span data-ttu-id="d0f58-151">In the Azure portal, on the **PurelyHR** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d0f58-151">In the Azure portal, on the **PurelyHR** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="d0f58-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d0f58-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/purelyhr-tutorial/tutorial_purelyhr_samlbase.png)

1. <span data-ttu-id="d0f58-155">On the **PurelyHR Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="d0f58-155">On the **PurelyHR Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/purelyhr-tutorial/tutorial_purelyhr_url.png)
   
    <span data-ttu-id="d0f58-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyID>.purelyhr.com/sso-consume`</span><span class="sxs-lookup"><span data-stu-id="d0f58-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyID>.purelyhr.com/sso-consume`</span></span>

1. <span data-ttu-id="d0f58-158">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="d0f58-158">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/purelyhr-tutorial/tutorial_purelyhr_url1.png)
    
    <span data-ttu-id="d0f58-160">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<companyID>.purelyhr.com/sso-initiate`</span><span class="sxs-lookup"><span data-stu-id="d0f58-160">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<companyID>.purelyhr.com/sso-initiate`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="d0f58-161">These values are not the real.</span><span class="sxs-lookup"><span data-stu-id="d0f58-161">These values are not the real.</span></span> <span data-ttu-id="d0f58-162">Update these values with the actual Reply URL and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="d0f58-162">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="d0f58-163">Contact [PurelyHR Client support team](http://support.purelyhr.com/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="d0f58-163">Contact [PurelyHR Client support team](http://support.purelyhr.com/) to get these values.</span></span> 

1. <span data-ttu-id="d0f58-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d0f58-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/purelyhr-tutorial/tutorial_purelyhr_certificate.png) 

1. <span data-ttu-id="d0f58-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="d0f58-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/purelyhr-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="d0f58-168">On the **PurelyHR Configuration** section, click **Configure PurelyHR** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="d0f58-168">On the **PurelyHR Configuration** section, click **Configure PurelyHR** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d0f58-169">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="d0f58-169">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/purelyhr-tutorial/tutorial_purelyhr_configure.png) 

1. <span data-ttu-id="d0f58-171">To configure single sign-on on **PurelyHR** side, login to their website as an administrator.</span><span class="sxs-lookup"><span data-stu-id="d0f58-171">To configure single sign-on on **PurelyHR** side, login to their website as an administrator.</span></span>

1. <span data-ttu-id="d0f58-172">Open the **Dashboard** from the options in the toolbar and click **SSO Settings**.</span><span class="sxs-lookup"><span data-stu-id="d0f58-172">Open the **Dashboard** from the options in the toolbar and click **SSO Settings**.</span></span>

1. <span data-ttu-id="d0f58-173">Paste the values in the boxes as described below-</span><span class="sxs-lookup"><span data-stu-id="d0f58-173">Paste the values in the boxes as described below-</span></span>

    ![Configure Single Sign-On](./media/purelyhr-tutorial/purelyhr-dashboard-sso-settings.png)  

    <span data-ttu-id="d0f58-175">a.</span><span class="sxs-lookup"><span data-stu-id="d0f58-175">a.</span></span> <span data-ttu-id="d0f58-176">Open the **Certificate(Bas64)** downloaded from the Azure portal in notepad and copy the certificate value.</span><span class="sxs-lookup"><span data-stu-id="d0f58-176">Open the **Certificate(Bas64)** downloaded from the Azure portal in notepad and copy the certificate value.</span></span> <span data-ttu-id="d0f58-177">Paste the copied value into the **X.509 Certificate** box.</span><span class="sxs-lookup"><span data-stu-id="d0f58-177">Paste the copied value into the **X.509 Certificate** box.</span></span>

    <span data-ttu-id="d0f58-178">b.</span><span class="sxs-lookup"><span data-stu-id="d0f58-178">b.</span></span> <span data-ttu-id="d0f58-179">In the **Idp Issuer URL** box, paste the **SAML Entity ID** copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d0f58-179">In the **Idp Issuer URL** box, paste the **SAML Entity ID** copied from the Azure portal.</span></span>

    <span data-ttu-id="d0f58-180">c.</span><span class="sxs-lookup"><span data-stu-id="d0f58-180">c.</span></span> <span data-ttu-id="d0f58-181">In the **Idp Endpoint URL** box, paste the **SAML Single Sign-On Service URL** copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d0f58-181">In the **Idp Endpoint URL** box, paste the **SAML Single Sign-On Service URL** copied from the Azure portal.</span></span> 

    <span data-ttu-id="d0f58-182">d.</span><span class="sxs-lookup"><span data-stu-id="d0f58-182">d.</span></span> <span data-ttu-id="d0f58-183">Check the **Auto-Create Users** checkbox to enable automatic user provisioning in PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="d0f58-183">Check the **Auto-Create Users** checkbox to enable automatic user provisioning in PurelyHR.</span></span>

    <span data-ttu-id="d0f58-184">e.</span><span class="sxs-lookup"><span data-stu-id="d0f58-184">e.</span></span> <span data-ttu-id="d0f58-185">Click **Save Changes** to save the settings.</span><span class="sxs-lookup"><span data-stu-id="d0f58-185">Click **Save Changes** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="d0f58-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="d0f58-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d0f58-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="d0f58-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d0f58-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d0f58-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d0f58-189">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d0f58-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="d0f58-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d0f58-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="d0f58-192">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d0f58-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d0f58-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d0f58-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/purelyhr-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="d0f58-195">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="d0f58-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/purelyhr-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="d0f58-197">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="d0f58-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/purelyhr-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="d0f58-199">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d0f58-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/purelyhr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d0f58-201">a.</span><span class="sxs-lookup"><span data-stu-id="d0f58-201">a.</span></span> <span data-ttu-id="d0f58-202">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d0f58-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d0f58-203">b.</span><span class="sxs-lookup"><span data-stu-id="d0f58-203">b.</span></span> <span data-ttu-id="d0f58-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d0f58-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d0f58-205">c.</span><span class="sxs-lookup"><span data-stu-id="d0f58-205">c.</span></span> <span data-ttu-id="d0f58-206">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="d0f58-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d0f58-207">d.</span><span class="sxs-lookup"><span data-stu-id="d0f58-207">d.</span></span> <span data-ttu-id="d0f58-208">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d0f58-208">Click **Create**.</span></span>
 
### <a name="creating-a-purelyhr-test-user"></a><span data-ttu-id="d0f58-209">Creating a PurelyHR test user</span><span class="sxs-lookup"><span data-stu-id="d0f58-209">Creating a PurelyHR test user</span></span>

<span data-ttu-id="d0f58-210">To enable Azure AD users to log in to PurelyHR, they must be provisioned into PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="d0f58-210">To enable Azure AD users to log in to PurelyHR, they must be provisioned into PurelyHR.</span></span> <span data-ttu-id="d0f58-211">In PurelyHR, provisioning is an automatic task and no manual steps are required when automatic user provisioning is enabled.</span><span class="sxs-lookup"><span data-stu-id="d0f58-211">In PurelyHR, provisioning is an automatic task and no manual steps are required when automatic user provisioning is enabled.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d0f58-212">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d0f58-212">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d0f58-213">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="d0f58-213">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PurelyHR.</span></span>

![Assign User][200] 

<span data-ttu-id="d0f58-215">**To assign Britta Simon to PurelyHR, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d0f58-215">**To assign Britta Simon to PurelyHR, perform the following steps:**</span></span>

1. <span data-ttu-id="d0f58-216">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d0f58-216">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="d0f58-218">In the applications list, select **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="d0f58-218">In the applications list, select **PurelyHR**.</span></span>

    ![Configure Single Sign-On](./media/purelyhr-tutorial/tutorial_purelyhr_app.png) 

1. <span data-ttu-id="d0f58-220">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d0f58-220">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="d0f58-222">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="d0f58-222">Click **Add** button.</span></span> <span data-ttu-id="d0f58-223">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d0f58-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="d0f58-225">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="d0f58-225">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="d0f58-226">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="d0f58-226">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="d0f58-227">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d0f58-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d0f58-228">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="d0f58-228">Testing single sign-on</span></span>

<span data-ttu-id="d0f58-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d0f58-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d0f58-230">Click the Absorb LMS tile in the Access Panel, you get automatically signed-on to your Absorb LMS application.</span><span class="sxs-lookup"><span data-stu-id="d0f58-230">Click the Absorb LMS tile in the Access Panel, you get automatically signed-on to your Absorb LMS application.</span></span>

<span data-ttu-id="d0f58-231">For more information about the Access Panel, see.</span><span class="sxs-lookup"><span data-stu-id="d0f58-231">For more information about the Access Panel, see.</span></span> <span data-ttu-id="d0f58-232">[Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d0f58-232">[Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d0f58-233">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d0f58-233">Additional resources</span></span>

* [<span data-ttu-id="d0f58-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0f58-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="d0f58-235">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d0f58-235">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/purelyhr-tutorial/tutorial_general_01.png
[2]: ./media/purelyhr-tutorial/tutorial_general_02.png
[3]: ./media/purelyhr-tutorial/tutorial_general_03.png
[4]: ./media/purelyhr-tutorial/tutorial_general_04.png

[100]: ./media/purelyhr-tutorial/tutorial_general_100.png

[200]: ./media/purelyhr-tutorial/tutorial_general_200.png
[201]: ./media/purelyhr-tutorial/tutorial_general_201.png
[202]: ./media/purelyhr-tutorial/tutorial_general_202.png
[203]: ./media/purelyhr-tutorial/tutorial_general_203.png

