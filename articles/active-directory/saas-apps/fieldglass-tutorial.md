---
title: 'Tutorial: Azure Active Directory integration with Fieldglass | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Fieldglass.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 2510195f-d5b1-4684-b3da-283fb8619df2
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: a14aeb55d9e5756660708e9e63a867a66a54a7b6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856221"
---
# <a name="tutorial-azure-active-directory-integration-with-fieldglass"></a><span data-ttu-id="8df60-103">Tutorial: Azure Active Directory integration with Fieldglass</span><span class="sxs-lookup"><span data-stu-id="8df60-103">Tutorial: Azure Active Directory integration with Fieldglass</span></span>

<span data-ttu-id="8df60-104">In this tutorial, you learn how to integrate Fieldglass with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8df60-104">In this tutorial, you learn how to integrate Fieldglass with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8df60-105">Integrating Fieldglass with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8df60-105">Integrating Fieldglass with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8df60-106">You can control in Azure AD who has access to Fieldglass</span><span class="sxs-lookup"><span data-stu-id="8df60-106">You can control in Azure AD who has access to Fieldglass</span></span>
- <span data-ttu-id="8df60-107">You can enable your users to automatically get signed-on to Fieldglass (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="8df60-107">You can enable your users to automatically get signed-on to Fieldglass (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8df60-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8df60-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8df60-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="8df60-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8df60-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8df60-110">Prerequisites</span></span>

<span data-ttu-id="8df60-111">To configure Azure AD integration with Fieldglass, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8df60-111">To configure Azure AD integration with Fieldglass, you need the following items:</span></span>

- <span data-ttu-id="8df60-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8df60-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8df60-113">A Fieldglass single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8df60-113">A Fieldglass single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8df60-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8df60-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8df60-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8df60-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8df60-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="8df60-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8df60-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8df60-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8df60-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8df60-118">Scenario description</span></span>
<span data-ttu-id="8df60-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8df60-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8df60-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8df60-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8df60-121">Adding Fieldglass from the gallery</span><span class="sxs-lookup"><span data-stu-id="8df60-121">Adding Fieldglass from the gallery</span></span>
1. <span data-ttu-id="8df60-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8df60-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fieldglass-from-the-gallery"></a><span data-ttu-id="8df60-123">Adding Fieldglass from the gallery</span><span class="sxs-lookup"><span data-stu-id="8df60-123">Adding Fieldglass from the gallery</span></span>
<span data-ttu-id="8df60-124">To configure the integration of Fieldglass into Azure AD, you need to add Fieldglass from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8df60-124">To configure the integration of Fieldglass into Azure AD, you need to add Fieldglass from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8df60-125">**To add Fieldglass from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8df60-125">**To add Fieldglass from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8df60-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8df60-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="8df60-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="8df60-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8df60-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8df60-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="8df60-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="8df60-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="8df60-133">In the search box, type **Fieldglass**.</span><span class="sxs-lookup"><span data-stu-id="8df60-133">In the search box, type **Fieldglass**.</span></span>

    ![Creating an Azure AD test user](./media/fieldglass-tutorial/tutorial_fieldglass_search.png)

1. <span data-ttu-id="8df60-135">In the results panel, select **Fieldglass**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="8df60-135">In the results panel, select **Fieldglass**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/fieldglass-tutorial/tutorial_fieldglass_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8df60-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8df60-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8df60-138">In this section, you configure and test Azure AD single sign-on with Fieldglass based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="8df60-138">In this section, you configure and test Azure AD single sign-on with Fieldglass based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8df60-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Fieldglass is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8df60-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Fieldglass is to a user in Azure AD.</span></span> <span data-ttu-id="8df60-140">In other words, a link relationship between an Azure AD user and the related user in Fieldglass needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8df60-140">In other words, a link relationship between an Azure AD user and the related user in Fieldglass needs to be established.</span></span>

<span data-ttu-id="8df60-141">In Fieldglass, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="8df60-141">In Fieldglass, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8df60-142">To configure and test Azure AD single sign-on with Fieldglass, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8df60-142">To configure and test Azure AD single sign-on with Fieldglass, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8df60-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8df60-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="8df60-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8df60-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="8df60-145">**[Creating a Fieldglass test user](#creating-a-fieldglass-test-user)** - to have a counterpart of Britta Simon in Fieldglass that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="8df60-145">**[Creating a Fieldglass test user](#creating-a-fieldglass-test-user)** - to have a counterpart of Britta Simon in Fieldglass that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="8df60-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8df60-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="8df60-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8df60-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8df60-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8df60-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8df60-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Fieldglass application.</span><span class="sxs-lookup"><span data-stu-id="8df60-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Fieldglass application.</span></span>

<span data-ttu-id="8df60-150">**To configure Azure AD single sign-on with Fieldglass, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8df60-150">**To configure Azure AD single sign-on with Fieldglass, perform the following steps:**</span></span>

1. <span data-ttu-id="8df60-151">In the Azure portal, on the **Fieldglass** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8df60-151">In the Azure portal, on the **Fieldglass** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="8df60-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8df60-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/fieldglass-tutorial/tutorial_fieldglass_samlbase.png)

1. <span data-ttu-id="8df60-155">On the **Fieldglass Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8df60-155">On the **Fieldglass Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/fieldglass-tutorial/tutorial_fieldglass_url.png)

    <span data-ttu-id="8df60-157">a.</span><span class="sxs-lookup"><span data-stu-id="8df60-157">a.</span></span> <span data-ttu-id="8df60-158">In the **Identifier** textbox, type a URL as  `https://www.fieldglass.com` or follow the pattern:  `https://<company name>.fgvms.com`</span><span class="sxs-lookup"><span data-stu-id="8df60-158">In the **Identifier** textbox, type a URL as  `https://www.fieldglass.com` or follow the pattern:  `https://<company name>.fgvms.com`</span></span>

    <span data-ttu-id="8df60-159">b.</span><span class="sxs-lookup"><span data-stu-id="8df60-159">b.</span></span> <span data-ttu-id="8df60-160">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="8df60-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://www.fieldglass.net/<company name>`|
    | `https://<company name>.fgvms.com/<company name>`|

    > [!NOTE] 
    > <span data-ttu-id="8df60-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="8df60-161">These values are not real.</span></span> <span data-ttu-id="8df60-162">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="8df60-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="8df60-163">Contact [Fieldglass support team](https://www.fieldglass.com/customer-support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="8df60-163">Contact [Fieldglass support team](https://www.fieldglass.com/customer-support) to get these values.</span></span>
 
1. <span data-ttu-id="8df60-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8df60-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/fieldglass-tutorial/tutorial_fieldglass_certificate.png) 

1. <span data-ttu-id="8df60-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="8df60-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/fieldglass-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="8df60-168">On the **Fieldglass Configuration** section, click **Configure Fieldglass** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="8df60-168">On the **Fieldglass Configuration** section, click **Configure Fieldglass** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8df60-169">Copy the **Sign-Out URL and SAML Entity ID** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="8df60-169">Copy the **Sign-Out URL and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/fieldglass-tutorial/tutorial_fieldglass_configure.png) 

1. <span data-ttu-id="8df60-171">To configure single sign-on on **Fieldglass** side, you need to send the downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID** to [Fieldglass support team](https://www.fieldglass.com/customer-support).</span><span class="sxs-lookup"><span data-stu-id="8df60-171">To configure single sign-on on **Fieldglass** side, you need to send the downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID** to [Fieldglass support team](https://www.fieldglass.com/customer-support).</span></span> <span data-ttu-id="8df60-172">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="8df60-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8df60-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="8df60-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8df60-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="8df60-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8df60-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8df60-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8df60-176">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8df60-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="8df60-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8df60-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="8df60-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8df60-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8df60-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8df60-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/fieldglass-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="8df60-182">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="8df60-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/fieldglass-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="8df60-184">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="8df60-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/fieldglass-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="8df60-186">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8df60-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/fieldglass-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8df60-188">a.</span><span class="sxs-lookup"><span data-stu-id="8df60-188">a.</span></span> <span data-ttu-id="8df60-189">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8df60-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8df60-190">b.</span><span class="sxs-lookup"><span data-stu-id="8df60-190">b.</span></span> <span data-ttu-id="8df60-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8df60-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8df60-192">c.</span><span class="sxs-lookup"><span data-stu-id="8df60-192">c.</span></span> <span data-ttu-id="8df60-193">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="8df60-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8df60-194">d.</span><span class="sxs-lookup"><span data-stu-id="8df60-194">d.</span></span> <span data-ttu-id="8df60-195">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8df60-195">Click **Create**.</span></span>
 
### <a name="creating-a-fieldglass-test-user"></a><span data-ttu-id="8df60-196">Creating a Fieldglass test user</span><span class="sxs-lookup"><span data-stu-id="8df60-196">Creating a Fieldglass test user</span></span>

<span data-ttu-id="8df60-197">The objective of this section is to create a user called Britta Simon in FieldGlass.</span><span class="sxs-lookup"><span data-stu-id="8df60-197">The objective of this section is to create a user called Britta Simon in FieldGlass.</span></span> <span data-ttu-id="8df60-198">Please work with your [Fieldglass support team](https://www.fieldglass.com/customer-support) to add the users in the Fieldglass account.</span><span class="sxs-lookup"><span data-stu-id="8df60-198">Please work with your [Fieldglass support team](https://www.fieldglass.com/customer-support) to add the users in the Fieldglass account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8df60-199">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8df60-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8df60-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Fieldglass.</span><span class="sxs-lookup"><span data-stu-id="8df60-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Fieldglass.</span></span>

![Assign User][200] 

<span data-ttu-id="8df60-202">**To assign Britta Simon to Fieldglass, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8df60-202">**To assign Britta Simon to Fieldglass, perform the following steps:**</span></span>

1. <span data-ttu-id="8df60-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8df60-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="8df60-205">In the applications list, select **Fieldglass**.</span><span class="sxs-lookup"><span data-stu-id="8df60-205">In the applications list, select **Fieldglass**.</span></span>

    ![Configure Single Sign-On](./media/fieldglass-tutorial/tutorial_fieldglass_app.png) 

1. <span data-ttu-id="8df60-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="8df60-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="8df60-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="8df60-209">Click **Add** button.</span></span> <span data-ttu-id="8df60-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8df60-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="8df60-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="8df60-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="8df60-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="8df60-213">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="8df60-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8df60-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8df60-215">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="8df60-215">Testing single sign-on</span></span>

<span data-ttu-id="8df60-216">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8df60-216">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8df60-217">When you click the Fieldglass tile in the Access Panel, you should get automatically signed-on to your Fieldglass application.</span><span class="sxs-lookup"><span data-stu-id="8df60-217">When you click the Fieldglass tile in the Access Panel, you should get automatically signed-on to your Fieldglass application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8df60-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8df60-218">Additional resources</span></span>

* [<span data-ttu-id="8df60-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8df60-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="8df60-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8df60-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/fieldglass-tutorial/tutorial_general_01.png
[2]: ./media/fieldglass-tutorial/tutorial_general_02.png
[3]: ./media/fieldglass-tutorial/tutorial_general_03.png
[4]: ./media/fieldglass-tutorial/tutorial_general_04.png

[100]: ./media/fieldglass-tutorial/tutorial_general_100.png

[200]: ./media/fieldglass-tutorial/tutorial_general_200.png
[201]: ./media/fieldglass-tutorial/tutorial_general_201.png
[202]: ./media/fieldglass-tutorial/tutorial_general_202.png
[203]: ./media/fieldglass-tutorial/tutorial_general_203.png

