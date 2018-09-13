---
title: 'Tutorial: Azure Active Directory integration with Bridge | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Bridge.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 3dbb6499-80c1-4d00-a0b4-e0ad5522cf0f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 4d15cbb4d0aa2905f36f88565690e359c1942ff4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865795"
---
# <a name="tutorial-azure-active-directory-integration-with-bridge"></a><span data-ttu-id="a6bcb-103">Tutorial: Azure Active Directory integration with Bridge</span><span class="sxs-lookup"><span data-stu-id="a6bcb-103">Tutorial: Azure Active Directory integration with Bridge</span></span>

<span data-ttu-id="a6bcb-104">In this tutorial, you learn how to integrate Bridge with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a6bcb-104">In this tutorial, you learn how to integrate Bridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a6bcb-105">Integrating Bridge with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a6bcb-105">Integrating Bridge with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a6bcb-106">You can control in Azure AD who has access to Bridge</span><span class="sxs-lookup"><span data-stu-id="a6bcb-106">You can control in Azure AD who has access to Bridge</span></span>
- <span data-ttu-id="a6bcb-107">You can enable your users to automatically get signed-on to Bridge (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="a6bcb-107">You can enable your users to automatically get signed-on to Bridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a6bcb-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a6bcb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a6bcb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a6bcb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6bcb-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a6bcb-110">Prerequisites</span></span>

<span data-ttu-id="a6bcb-111">To configure Azure AD integration with Bridge, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a6bcb-111">To configure Azure AD integration with Bridge, you need the following items:</span></span>

- <span data-ttu-id="a6bcb-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a6bcb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a6bcb-113">A Bridge single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a6bcb-113">A Bridge single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a6bcb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a6bcb-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a6bcb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a6bcb-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a6bcb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a6bcb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a6bcb-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a6bcb-118">Scenario description</span></span>
<span data-ttu-id="a6bcb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a6bcb-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a6bcb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a6bcb-121">Adding Bridge from the gallery</span><span class="sxs-lookup"><span data-stu-id="a6bcb-121">Adding Bridge from the gallery</span></span>
1. <span data-ttu-id="a6bcb-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a6bcb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bridge-from-the-gallery"></a><span data-ttu-id="a6bcb-123">Adding Bridge from the gallery</span><span class="sxs-lookup"><span data-stu-id="a6bcb-123">Adding Bridge from the gallery</span></span>
<span data-ttu-id="a6bcb-124">To configure the integration of Bridge into Azure AD, you need to add Bridge from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-124">To configure the integration of Bridge into Azure AD, you need to add Bridge from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a6bcb-125">**To add Bridge from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a6bcb-125">**To add Bridge from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a6bcb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="a6bcb-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a6bcb-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="a6bcb-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="a6bcb-133">In the search box, type **Bridge**.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-133">In the search box, type **Bridge**.</span></span>

    ![Creating an Azure AD test user](./media/bridge-tutorial/tutorial_bridge_search.png)

1. <span data-ttu-id="a6bcb-135">In the results panel, select **Bridge**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-135">In the results panel, select **Bridge**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/bridge-tutorial/tutorial_bridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a6bcb-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a6bcb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a6bcb-138">In this section, you configure and test Azure AD single sign-on with Bridge based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a6bcb-138">In this section, you configure and test Azure AD single sign-on with Bridge based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a6bcb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bridge is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bridge is to a user in Azure AD.</span></span> <span data-ttu-id="a6bcb-140">In other words, a link relationship between an Azure AD user and the related user in Bridge needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-140">In other words, a link relationship between an Azure AD user and the related user in Bridge needs to be established.</span></span>

<span data-ttu-id="a6bcb-141">In Bridge, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-141">In Bridge, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a6bcb-142">To configure and test Azure AD single sign-on with Bridge, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a6bcb-142">To configure and test Azure AD single sign-on with Bridge, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a6bcb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="a6bcb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="a6bcb-145">**[Creating a Bridge test user](#creating-a-bridge-test-user)** - to have a counterpart of Britta Simon in Bridge that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-145">**[Creating a Bridge test user](#creating-a-bridge-test-user)** - to have a counterpart of Britta Simon in Bridge that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="a6bcb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="a6bcb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a6bcb-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a6bcb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a6bcb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bridge application.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bridge application.</span></span>

<span data-ttu-id="a6bcb-150">**To configure Azure AD single sign-on with Bridge, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a6bcb-150">**To configure Azure AD single sign-on with Bridge, perform the following steps:**</span></span>

1. <span data-ttu-id="a6bcb-151">In the Azure portal, on the **Bridge** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-151">In the Azure portal, on the **Bridge** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="a6bcb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/bridge-tutorial/tutorial_bridge_samlbase.png)

1. <span data-ttu-id="a6bcb-155">On the **Bridge Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a6bcb-155">On the **Bridge Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/bridge-tutorial/tutorial_bridge_url.png)

    <span data-ttu-id="a6bcb-157">a.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-157">a.</span></span> <span data-ttu-id="a6bcb-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.bridgeapp.com`</span><span class="sxs-lookup"><span data-stu-id="a6bcb-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.bridgeapp.com`</span></span>

    <span data-ttu-id="a6bcb-159">b.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-159">b.</span></span> <span data-ttu-id="a6bcb-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.bridgeapp.com`</span><span class="sxs-lookup"><span data-stu-id="a6bcb-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.bridgeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a6bcb-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-161">These values are not real.</span></span> <span data-ttu-id="a6bcb-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a6bcb-163">Contact [Bridge Client support team](https://community.bridgeapp.com/community/help) to get these values.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-163">Contact [Bridge Client support team](https://community.bridgeapp.com/community/help) to get these values.</span></span> 
 
1. <span data-ttu-id="a6bcb-164">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-164">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/bridge-tutorial/tutorial_bridge_certificate.png) 

1. <span data-ttu-id="a6bcb-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/bridge-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="a6bcb-168">On the **Bridge Configuration** section, click **Configure Bridge** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-168">On the **Bridge Configuration** section, click **Configure Bridge** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a6bcb-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="a6bcb-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/bridge-tutorial/tutorial_bridge_configure.png) 

1. <span data-ttu-id="a6bcb-171">To configure single sign-on on **Bridge** side, you need to send the downloaded **Certificate(Raw)** and **SAML Entity ID, SAML Single Sign-On Service URL, and Sign-Out URL** to [Bridge support team](https://community.bridgeapp.com/community/help).</span><span class="sxs-lookup"><span data-stu-id="a6bcb-171">To configure single sign-on on **Bridge** side, you need to send the downloaded **Certificate(Raw)** and **SAML Entity ID, SAML Single Sign-On Service URL, and Sign-Out URL** to [Bridge support team](https://community.bridgeapp.com/community/help).</span></span> 

> [!TIP]
> <span data-ttu-id="a6bcb-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="a6bcb-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a6bcb-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a6bcb-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a6bcb-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a6bcb-175">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a6bcb-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="a6bcb-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="a6bcb-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a6bcb-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a6bcb-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/bridge-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="a6bcb-181">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/bridge-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="a6bcb-183">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/bridge-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="a6bcb-185">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a6bcb-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/bridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a6bcb-187">a.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-187">a.</span></span> <span data-ttu-id="a6bcb-188">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a6bcb-189">b.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-189">b.</span></span> <span data-ttu-id="a6bcb-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a6bcb-191">c.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-191">c.</span></span> <span data-ttu-id="a6bcb-192">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a6bcb-193">d.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-193">d.</span></span> <span data-ttu-id="a6bcb-194">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-194">Click **Create**.</span></span>
 
### <a name="creating-a-bridge-test-user"></a><span data-ttu-id="a6bcb-195">Creating a Bridge test user</span><span class="sxs-lookup"><span data-stu-id="a6bcb-195">Creating a Bridge test user</span></span>

<span data-ttu-id="a6bcb-196">In this section, you create a user called Britta Simon in Bridge.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-196">In this section, you create a user called Britta Simon in Bridge.</span></span> <span data-ttu-id="a6bcb-197">Work with [Bridge Client support team](https://community.bridgeapp.com/community/help) to create a user in the platform.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-197">Work with [Bridge Client support team](https://community.bridgeapp.com/community/help) to create a user in the platform.</span></span> <span data-ttu-id="a6bcb-198">You can raise the support ticket with Bridge from <a href="https://community.bridgeapp.com/community/help">here</a> to add the users in the Bridge platform.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-198">You can raise the support ticket with Bridge from <a href="https://community.bridgeapp.com/community/help">here</a> to add the users in the Bridge platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a6bcb-199">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a6bcb-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a6bcb-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bridge.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bridge.</span></span>

![Assign User][200] 

<span data-ttu-id="a6bcb-202">**To assign Britta Simon to Bridge, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a6bcb-202">**To assign Britta Simon to Bridge, perform the following steps:**</span></span>

1. <span data-ttu-id="a6bcb-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="a6bcb-205">In the applications list, select **Bridge**.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-205">In the applications list, select **Bridge**.</span></span>

    ![Configure Single Sign-On](./media/bridge-tutorial/tutorial_bridge_app.png) 

1. <span data-ttu-id="a6bcb-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="a6bcb-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-209">Click **Add** button.</span></span> <span data-ttu-id="a6bcb-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="a6bcb-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="a6bcb-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-213">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="a6bcb-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a6bcb-215">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="a6bcb-215">Testing single sign-on</span></span>

<span data-ttu-id="a6bcb-216">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-216">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="a6bcb-217">When you click the Bridge tile in the Access Panel, you should get automatically signed-on to your Bridge application.</span><span class="sxs-lookup"><span data-stu-id="a6bcb-217">When you click the Bridge tile in the Access Panel, you should get automatically signed-on to your Bridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a6bcb-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a6bcb-218">Additional resources</span></span>

* [<span data-ttu-id="a6bcb-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6bcb-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a6bcb-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a6bcb-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/bridge-tutorial/tutorial_general_01.png
[2]: ./media/bridge-tutorial/tutorial_general_02.png
[3]: ./media/bridge-tutorial/tutorial_general_03.png
[4]: ./media/bridge-tutorial/tutorial_general_04.png

[100]: ./media/bridge-tutorial/tutorial_general_100.png

[200]: ./media/bridge-tutorial/tutorial_general_200.png
[201]: ./media/bridge-tutorial/tutorial_general_201.png
[202]: ./media/bridge-tutorial/tutorial_general_202.png
[203]: ./media/bridge-tutorial/tutorial_general_203.png

