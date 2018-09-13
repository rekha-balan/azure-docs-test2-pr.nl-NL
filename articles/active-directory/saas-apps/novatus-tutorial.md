---
title: 'Tutorial: Azure Active Directory integration with Novatus | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Novatus.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: d2f13779-bdb7-4408-9738-be67ed3de4e5
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: jeedes
ms.openlocfilehash: 8ad4a59884fb2ca35fd594aba3f8aa8860827afd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869532"
---
# <a name="tutorial-azure-active-directory-integration-with-novatus"></a><span data-ttu-id="37c30-103">Tutorial: Azure Active Directory integration with Novatus</span><span class="sxs-lookup"><span data-stu-id="37c30-103">Tutorial: Azure Active Directory integration with Novatus</span></span>

<span data-ttu-id="37c30-104">In this tutorial, you learn how to integrate Novatus with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="37c30-104">In this tutorial, you learn how to integrate Novatus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="37c30-105">Integrating Novatus with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="37c30-105">Integrating Novatus with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="37c30-106">You can control in Azure AD who has access to Novatus</span><span class="sxs-lookup"><span data-stu-id="37c30-106">You can control in Azure AD who has access to Novatus</span></span>
- <span data-ttu-id="37c30-107">You can enable your users to automatically get signed-on to Novatus (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="37c30-107">You can enable your users to automatically get signed-on to Novatus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="37c30-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="37c30-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="37c30-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="37c30-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37c30-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="37c30-110">Prerequisites</span></span>

<span data-ttu-id="37c30-111">To configure Azure AD integration with Novatus, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="37c30-111">To configure Azure AD integration with Novatus, you need the following items:</span></span>

- <span data-ttu-id="37c30-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="37c30-112">An Azure AD subscription</span></span>
- <span data-ttu-id="37c30-113">A Novatus single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="37c30-113">A Novatus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="37c30-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="37c30-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="37c30-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="37c30-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="37c30-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="37c30-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="37c30-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="37c30-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="37c30-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="37c30-118">Scenario description</span></span>
<span data-ttu-id="37c30-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="37c30-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="37c30-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="37c30-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="37c30-121">Adding Novatus from the gallery</span><span class="sxs-lookup"><span data-stu-id="37c30-121">Adding Novatus from the gallery</span></span>
1. <span data-ttu-id="37c30-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="37c30-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-novatus-from-the-gallery"></a><span data-ttu-id="37c30-123">Adding Novatus from the gallery</span><span class="sxs-lookup"><span data-stu-id="37c30-123">Adding Novatus from the gallery</span></span>
<span data-ttu-id="37c30-124">To configure the integration of Novatus into Azure AD, you need to add Novatus from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="37c30-124">To configure the integration of Novatus into Azure AD, you need to add Novatus from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="37c30-125">**To add Novatus from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="37c30-125">**To add Novatus from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="37c30-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="37c30-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="37c30-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="37c30-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="37c30-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="37c30-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="37c30-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="37c30-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="37c30-133">In the search box, type **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="37c30-133">In the search box, type **Novatus**.</span></span>

    ![Creating an Azure AD test user](./media/novatus-tutorial/tutorial_novatus_search.png)

1. <span data-ttu-id="37c30-135">In the results panel, select **Novatus**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="37c30-135">In the results panel, select **Novatus**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/novatus-tutorial/tutorial_novatus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="37c30-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="37c30-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="37c30-138">In this section, you configure and test Azure AD single sign-on with Novatus based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="37c30-138">In this section, you configure and test Azure AD single sign-on with Novatus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="37c30-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Novatus is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37c30-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Novatus is to a user in Azure AD.</span></span> <span data-ttu-id="37c30-140">In other words, a link relationship between an Azure AD user and the related user in Novatus needs to be established.</span><span class="sxs-lookup"><span data-stu-id="37c30-140">In other words, a link relationship between an Azure AD user and the related user in Novatus needs to be established.</span></span>

<span data-ttu-id="37c30-141">In Novatus, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="37c30-141">In Novatus, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="37c30-142">To configure and test Azure AD single sign-on with Novatus, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="37c30-142">To configure and test Azure AD single sign-on with Novatus, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="37c30-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="37c30-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="37c30-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37c30-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="37c30-145">**[Creating a Novatus test user](#creating-a-novatus-test-user)** - to have a counterpart of Britta Simon in Novatus that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="37c30-145">**[Creating a Novatus test user](#creating-a-novatus-test-user)** - to have a counterpart of Britta Simon in Novatus that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="37c30-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="37c30-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="37c30-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="37c30-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="37c30-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="37c30-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="37c30-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Novatus application.</span><span class="sxs-lookup"><span data-stu-id="37c30-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Novatus application.</span></span>

<span data-ttu-id="37c30-150">**To configure Azure AD single sign-on with Novatus, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="37c30-150">**To configure Azure AD single sign-on with Novatus, perform the following steps:**</span></span>

1. <span data-ttu-id="37c30-151">In the Azure portal, on the **Novatus** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="37c30-151">In the Azure portal, on the **Novatus** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="37c30-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="37c30-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/novatus-tutorial/tutorial_novatus_samlbase.png)

1. <span data-ttu-id="37c30-155">On the **Novatus Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="37c30-155">On the **Novatus Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/novatus-tutorial/tutorial_novatus_url.png)

     <span data-ttu-id="37c30-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.novatuscontracts.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="37c30-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.novatuscontracts.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="37c30-158">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="37c30-158">This value is not real.</span></span> <span data-ttu-id="37c30-159">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="37c30-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="37c30-160">Contact [Novatus Client support team](mailto:jvinci@novatusinc.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="37c30-160">Contact [Novatus Client support team](mailto:jvinci@novatusinc.com) to get this value.</span></span> 
 


1. <span data-ttu-id="37c30-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="37c30-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/novatus-tutorial/tutorial_novatus_certificate.png) 

1. <span data-ttu-id="37c30-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="37c30-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/novatus-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="37c30-165">On the **Novatus Configuration** section, click **Configure Novatus** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="37c30-165">On the **Novatus Configuration** section, click **Configure Novatus** to open **Configure sign-on** window.</span></span> <span data-ttu-id="37c30-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="37c30-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/novatus-tutorial/tutorial_novatus_configure.png) 

1. <span data-ttu-id="37c30-168">To get SSO configured for your application, contact your [Novatus support team](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="37c30-168">To get SSO configured for your application, contact your [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> <span data-ttu-id="37c30-169">Attach the **downloaded certificate** file to your mail and share the **metadata urls** (**Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL**) with Novatus team to set up SSO on their side.</span><span class="sxs-lookup"><span data-stu-id="37c30-169">Attach the **downloaded certificate** file to your mail and share the **metadata urls** (**Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL**) with Novatus team to set up SSO on their side.</span></span>

> [!TIP]
> <span data-ttu-id="37c30-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="37c30-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="37c30-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="37c30-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="37c30-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="37c30-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="37c30-173">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="37c30-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="37c30-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37c30-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="37c30-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="37c30-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="37c30-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="37c30-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/novatus-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="37c30-179">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="37c30-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/novatus-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="37c30-181">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="37c30-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/novatus-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="37c30-183">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="37c30-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/novatus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="37c30-185">a.</span><span class="sxs-lookup"><span data-stu-id="37c30-185">a.</span></span> <span data-ttu-id="37c30-186">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="37c30-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="37c30-187">b.</span><span class="sxs-lookup"><span data-stu-id="37c30-187">b.</span></span> <span data-ttu-id="37c30-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="37c30-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="37c30-189">c.</span><span class="sxs-lookup"><span data-stu-id="37c30-189">c.</span></span> <span data-ttu-id="37c30-190">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="37c30-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="37c30-191">d.</span><span class="sxs-lookup"><span data-stu-id="37c30-191">d.</span></span> <span data-ttu-id="37c30-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="37c30-192">Click **Create**.</span></span>
 
### <a name="creating-a-novatus-test-user"></a><span data-ttu-id="37c30-193">Creating a Novatus test user</span><span class="sxs-lookup"><span data-stu-id="37c30-193">Creating a Novatus test user</span></span>

<span data-ttu-id="37c30-194">The objective of this section is to create a user called Britta Simon in Novatus.</span><span class="sxs-lookup"><span data-stu-id="37c30-194">The objective of this section is to create a user called Britta Simon in Novatus.</span></span> <span data-ttu-id="37c30-195">Novatus supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="37c30-195">Novatus supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="37c30-196">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="37c30-196">There is no action item for you in this section.</span></span> <span data-ttu-id="37c30-197">A new user will be created during an attempt to access Novatus if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="37c30-197">A new user will be created during an attempt to access Novatus if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="37c30-198">If you need to create an user manually, you need to contact the [Novatus support team](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="37c30-198">If you need to create an user manually, you need to contact the [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="37c30-199">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="37c30-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="37c30-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Novatus.</span><span class="sxs-lookup"><span data-stu-id="37c30-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Novatus.</span></span>

![Assign User][200] 

<span data-ttu-id="37c30-202">**To assign Britta Simon to Novatus, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="37c30-202">**To assign Britta Simon to Novatus, perform the following steps:**</span></span>

1. <span data-ttu-id="37c30-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="37c30-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="37c30-205">In the applications list, select **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="37c30-205">In the applications list, select **Novatus**.</span></span>

    ![Configure Single Sign-On](./media/novatus-tutorial/tutorial_novatus_app.png) 

1. <span data-ttu-id="37c30-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="37c30-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="37c30-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="37c30-209">Click **Add** button.</span></span> <span data-ttu-id="37c30-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="37c30-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="37c30-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="37c30-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="37c30-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="37c30-213">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="37c30-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="37c30-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="37c30-215">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="37c30-215">Testing single sign-on</span></span>

<span data-ttu-id="37c30-216">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="37c30-216">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="37c30-217">When you click the Novatus tile in the Access Panel, you should get automatically signed-on to your Novatus application.</span><span class="sxs-lookup"><span data-stu-id="37c30-217">When you click the Novatus tile in the Access Panel, you should get automatically signed-on to your Novatus application.</span></span> <span data-ttu-id="37c30-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="37c30-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37c30-219">Additional resources</span><span class="sxs-lookup"><span data-stu-id="37c30-219">Additional resources</span></span>

* [<span data-ttu-id="37c30-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37c30-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="37c30-221">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="37c30-221">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/novatus-tutorial/tutorial_general_01.png
[2]: ./media/novatus-tutorial/tutorial_general_02.png
[3]: ./media/novatus-tutorial/tutorial_general_03.png
[4]: ./media/novatus-tutorial/tutorial_general_04.png

[100]: ./media/novatus-tutorial/tutorial_general_100.png

[200]: ./media/novatus-tutorial/tutorial_general_200.png
[201]: ./media/novatus-tutorial/tutorial_general_201.png
[202]: ./media/novatus-tutorial/tutorial_general_202.png
[203]: ./media/novatus-tutorial/tutorial_general_203.png

