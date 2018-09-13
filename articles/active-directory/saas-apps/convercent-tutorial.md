---
title: 'Tutorial: Azure Active Directory integration with Convercent | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Convercent.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: f9c9d290-0e13-490b-b559-0be772d6a690
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: add5be434ea8902de58dfdffc93b2c4829183667
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857211"
---
# <a name="tutorial-azure-active-directory-integration-with-convercent"></a><span data-ttu-id="9b42c-103">Tutorial: Azure Active Directory integration with Convercent</span><span class="sxs-lookup"><span data-stu-id="9b42c-103">Tutorial: Azure Active Directory integration with Convercent</span></span>

<span data-ttu-id="9b42c-104">In this tutorial, you learn how to integrate Convercent with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9b42c-104">In this tutorial, you learn how to integrate Convercent with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9b42c-105">Integrating Convercent with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="9b42c-105">Integrating Convercent with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9b42c-106">You can control in Azure AD who has access to Convercent</span><span class="sxs-lookup"><span data-stu-id="9b42c-106">You can control in Azure AD who has access to Convercent</span></span>
- <span data-ttu-id="9b42c-107">You can enable your users to automatically get signed-on to Convercent (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="9b42c-107">You can enable your users to automatically get signed-on to Convercent (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9b42c-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="9b42c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9b42c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="9b42c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b42c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9b42c-110">Prerequisites</span></span>

<span data-ttu-id="9b42c-111">To configure Azure AD integration with Convercent, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="9b42c-111">To configure Azure AD integration with Convercent, you need the following items:</span></span>

- <span data-ttu-id="9b42c-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="9b42c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9b42c-113">A Convercent single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="9b42c-113">A Convercent single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9b42c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="9b42c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9b42c-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="9b42c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9b42c-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="9b42c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9b42c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9b42c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9b42c-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="9b42c-118">Scenario description</span></span>
<span data-ttu-id="9b42c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="9b42c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9b42c-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="9b42c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9b42c-121">Adding Convercent from the gallery</span><span class="sxs-lookup"><span data-stu-id="9b42c-121">Adding Convercent from the gallery</span></span>
1. <span data-ttu-id="9b42c-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9b42c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-convercent-from-the-gallery"></a><span data-ttu-id="9b42c-123">Adding Convercent from the gallery</span><span class="sxs-lookup"><span data-stu-id="9b42c-123">Adding Convercent from the gallery</span></span>
<span data-ttu-id="9b42c-124">To configure the integration of Convercent into Azure AD, you need to add Convercent from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="9b42c-124">To configure the integration of Convercent into Azure AD, you need to add Convercent from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9b42c-125">**To add Convercent from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9b42c-125">**To add Convercent from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9b42c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9b42c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="9b42c-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="9b42c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9b42c-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9b42c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="9b42c-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="9b42c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="9b42c-133">In the search box, type **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="9b42c-133">In the search box, type **Convercent**.</span></span>

    ![Creating an Azure AD test user](./media/convercent-tutorial/tutorial_convercent_search.png)

1. <span data-ttu-id="9b42c-135">In the results panel, select **Convercent**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="9b42c-135">In the results panel, select **Convercent**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/convercent-tutorial/tutorial_convercent_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9b42c-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9b42c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9b42c-138">In this section, you configure and test Azure AD single sign-on with Convercent based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="9b42c-138">In this section, you configure and test Azure AD single sign-on with Convercent based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9b42c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Convercent is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b42c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Convercent is to a user in Azure AD.</span></span> <span data-ttu-id="9b42c-140">In other words, a link relationship between an Azure AD user and the related user in Convercent needs to be established.</span><span class="sxs-lookup"><span data-stu-id="9b42c-140">In other words, a link relationship between an Azure AD user and the related user in Convercent needs to be established.</span></span>

<span data-ttu-id="9b42c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Convercent.</span><span class="sxs-lookup"><span data-stu-id="9b42c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Convercent.</span></span>

<span data-ttu-id="9b42c-142">To configure and test Azure AD single sign-on with Convercent, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="9b42c-142">To configure and test Azure AD single sign-on with Convercent, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9b42c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="9b42c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="9b42c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9b42c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="9b42c-145">**[Creating a Convercent test user](#creating-a-convercent-test-user)** - to have a counterpart of Britta Simon in Convercent that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="9b42c-145">**[Creating a Convercent test user](#creating-a-convercent-test-user)** - to have a counterpart of Britta Simon in Convercent that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="9b42c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9b42c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="9b42c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="9b42c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9b42c-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9b42c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9b42c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Convercent application.</span><span class="sxs-lookup"><span data-stu-id="9b42c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Convercent application.</span></span>

<span data-ttu-id="9b42c-150">**To configure Azure AD single sign-on with Convercent, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9b42c-150">**To configure Azure AD single sign-on with Convercent, perform the following steps:**</span></span>

1. <span data-ttu-id="9b42c-151">In the Azure portal, on the **Convercent** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9b42c-151">In the Azure portal, on the **Convercent** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="9b42c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9b42c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/convercent-tutorial/tutorial_convercent_samlbase.png)

1. <span data-ttu-id="9b42c-155">On the **Convercent Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following step:</span><span class="sxs-lookup"><span data-stu-id="9b42c-155">On the **Convercent Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following step:</span></span>

    ![Configure Single Sign-On](./media/convercent-tutorial/tutorial_convercent_url.png)

    <span data-ttu-id="9b42c-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="9b42c-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.convercent.com/`</span></span>
 
1. <span data-ttu-id="9b42c-158">If you wish to configure the application in **SP initiated mode**, on the **Convercent Domain and URLs** section perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9b42c-158">If you wish to configure the application in **SP initiated mode**, on the **Convercent Domain and URLs** section perform the following steps:</span></span>
    
    ![Configure Single Sign-On](./media/convercent-tutorial/tutorial_convercent_url1.png)

     <span data-ttu-id="9b42c-160">a.</span><span class="sxs-lookup"><span data-stu-id="9b42c-160">a.</span></span> <span data-ttu-id="9b42c-161">Click **"Show advanced URL settings."**</span><span class="sxs-lookup"><span data-stu-id="9b42c-161">Click **"Show advanced URL settings."**</span></span> 

     <span data-ttu-id="9b42c-162">b.</span><span class="sxs-lookup"><span data-stu-id="9b42c-162">b.</span></span> <span data-ttu-id="9b42c-163">In the **Sign On URL** textbox, type the value using the following pattern: `https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="9b42c-163">In the **Sign On URL** textbox, type the value using the following pattern: `https://<instancename>.convercent.com/`</span></span>

     <span data-ttu-id="9b42c-164">c.</span><span class="sxs-lookup"><span data-stu-id="9b42c-164">c.</span></span> <span data-ttu-id="9b42c-165">In the **Relay State** textbox, type the value using the following pattern: `https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="9b42c-165">In the **Relay State** textbox, type the value using the following pattern: `https://<instancename>.convercent.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9b42c-166">These values are not the real values.</span><span class="sxs-lookup"><span data-stu-id="9b42c-166">These values are not the real values.</span></span> <span data-ttu-id="9b42c-167">Update these values with the actual Identifier, Sign On URL and Relay State.</span><span class="sxs-lookup"><span data-stu-id="9b42c-167">Update these values with the actual Identifier, Sign On URL and Relay State.</span></span> <span data-ttu-id="9b42c-168">Contact [Convercent Client support team](http://support.convercent.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="9b42c-168">Contact [Convercent Client support team](http://support.convercent.com) to get these values.</span></span>

1. <span data-ttu-id="9b42c-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="9b42c-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](./media/convercent-tutorial/tutorial_convercent_certificate.png) 

1. <span data-ttu-id="9b42c-171">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="9b42c-171">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/convercent-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="9b42c-173">To get SSO configured for your application, contact [Convercent support team](mailto:support@convercent.com) and provide them with the downloaded **Metadata XML**.</span><span class="sxs-lookup"><span data-stu-id="9b42c-173">To get SSO configured for your application, contact [Convercent support team](mailto:support@convercent.com) and provide them with the downloaded **Metadata XML**.</span></span>

> [!TIP]
> <span data-ttu-id="9b42c-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="9b42c-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9b42c-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="9b42c-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9b42c-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9b42c-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9b42c-177">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9b42c-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="9b42c-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9b42c-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="9b42c-180">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9b42c-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9b42c-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9b42c-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/convercent-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="9b42c-183">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="9b42c-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/convercent-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="9b42c-185">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="9b42c-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/convercent-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="9b42c-187">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9b42c-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/convercent-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9b42c-189">a.</span><span class="sxs-lookup"><span data-stu-id="9b42c-189">a.</span></span> <span data-ttu-id="9b42c-190">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9b42c-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9b42c-191">b.</span><span class="sxs-lookup"><span data-stu-id="9b42c-191">b.</span></span> <span data-ttu-id="9b42c-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9b42c-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9b42c-193">c.</span><span class="sxs-lookup"><span data-stu-id="9b42c-193">c.</span></span> <span data-ttu-id="9b42c-194">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="9b42c-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9b42c-195">d.</span><span class="sxs-lookup"><span data-stu-id="9b42c-195">d.</span></span> <span data-ttu-id="9b42c-196">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="9b42c-196">Click **Create**.</span></span>
 
### <a name="creating-a-convercent-test-user"></a><span data-ttu-id="9b42c-197">Creating a Convercent test user</span><span class="sxs-lookup"><span data-stu-id="9b42c-197">Creating a Convercent test user</span></span>

<span data-ttu-id="9b42c-198">Work with [Convercent support team](mailto:support@convercent.com) to add the users in the Convercent platform.</span><span class="sxs-lookup"><span data-stu-id="9b42c-198">Work with [Convercent support team](mailto:support@convercent.com) to add the users in the Convercent platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9b42c-199">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9b42c-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9b42c-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Convercent.</span><span class="sxs-lookup"><span data-stu-id="9b42c-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Convercent.</span></span>

![Assign User][200] 

<span data-ttu-id="9b42c-202">**To assign Britta Simon to Convercent, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9b42c-202">**To assign Britta Simon to Convercent, perform the following steps:**</span></span>

1. <span data-ttu-id="9b42c-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9b42c-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="9b42c-205">In the applications list, select **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="9b42c-205">In the applications list, select **Convercent**.</span></span>

    ![Configure Single Sign-On](./media/convercent-tutorial/tutorial_convercent_app.png) 

1. <span data-ttu-id="9b42c-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="9b42c-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="9b42c-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="9b42c-209">Click **Add** button.</span></span> <span data-ttu-id="9b42c-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9b42c-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="9b42c-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="9b42c-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="9b42c-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="9b42c-213">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="9b42c-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9b42c-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9b42c-215">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="9b42c-215">Testing single sign-on</span></span>

<span data-ttu-id="9b42c-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9b42c-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9b42c-217">When you click the Convercent tile in the Access Panel, you should get automatically signed-on to your Convercent application.</span><span class="sxs-lookup"><span data-stu-id="9b42c-217">When you click the Convercent tile in the Access Panel, you should get automatically signed-on to your Convercent application.</span></span>
<span data-ttu-id="9b42c-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9b42c-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9b42c-219">Additional resources</span><span class="sxs-lookup"><span data-stu-id="9b42c-219">Additional resources</span></span>

* [<span data-ttu-id="9b42c-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b42c-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="9b42c-221">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9b42c-221">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/convercent-tutorial/tutorial_general_01.png
[2]: ./media/convercent-tutorial/tutorial_general_02.png
[3]: ./media/convercent-tutorial/tutorial_general_03.png
[4]: ./media/convercent-tutorial/tutorial_general_04.png

[100]: ./media/convercent-tutorial/tutorial_general_100.png

[200]: ./media/convercent-tutorial/tutorial_general_200.png
[201]: ./media/convercent-tutorial/tutorial_general_201.png
[202]: ./media/convercent-tutorial/tutorial_general_202.png
[203]: ./media/convercent-tutorial/tutorial_general_203.png

