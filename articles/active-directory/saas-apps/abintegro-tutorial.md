---
title: 'Tutorial: Azure Active Directory integration with Abintegro | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Abintegro.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 99287e1f-4189-494a-97c8-e1c03d047fd3
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 70b9d41ff9ed47e9ac376f1e13627cc82d87130f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967146"
---
# <a name="tutorial-azure-active-directory-integration-with-abintegro"></a><span data-ttu-id="6a878-103">Tutorial: Azure Active Directory integration with Abintegro</span><span class="sxs-lookup"><span data-stu-id="6a878-103">Tutorial: Azure Active Directory integration with Abintegro</span></span>

<span data-ttu-id="6a878-104">In this tutorial, you learn how to integrate Abintegro with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6a878-104">In this tutorial, you learn how to integrate Abintegro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6a878-105">Integrating Abintegro with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="6a878-105">Integrating Abintegro with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6a878-106">You can control in Azure AD who has access to Abintegro</span><span class="sxs-lookup"><span data-stu-id="6a878-106">You can control in Azure AD who has access to Abintegro</span></span>
- <span data-ttu-id="6a878-107">You can enable your users to automatically get signed-on to Abintegro (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="6a878-107">You can enable your users to automatically get signed-on to Abintegro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6a878-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6a878-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6a878-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="6a878-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a878-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6a878-110">Prerequisites</span></span>

<span data-ttu-id="6a878-111">To configure Azure AD integration with Abintegro, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="6a878-111">To configure Azure AD integration with Abintegro, you need the following items:</span></span>

- <span data-ttu-id="6a878-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="6a878-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6a878-113">An Abintegro single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="6a878-113">An Abintegro single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6a878-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="6a878-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6a878-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="6a878-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6a878-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="6a878-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6a878-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6a878-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6a878-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="6a878-118">Scenario description</span></span>
<span data-ttu-id="6a878-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="6a878-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6a878-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="6a878-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6a878-121">Adding Abintegro from the gallery</span><span class="sxs-lookup"><span data-stu-id="6a878-121">Adding Abintegro from the gallery</span></span>
2. <span data-ttu-id="6a878-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6a878-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-abintegro-from-the-gallery"></a><span data-ttu-id="6a878-123">Adding Abintegro from the gallery</span><span class="sxs-lookup"><span data-stu-id="6a878-123">Adding Abintegro from the gallery</span></span>
<span data-ttu-id="6a878-124">To configure the integration of Abintegro into Azure AD, you need to add Abintegro from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="6a878-124">To configure the integration of Abintegro into Azure AD, you need to add Abintegro from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6a878-125">**To add Abintegro from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6a878-125">**To add Abintegro from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6a878-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="6a878-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6a878-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="6a878-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6a878-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6a878-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="6a878-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="6a878-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="6a878-133">In the search box, type **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="6a878-133">In the search box, type **Abintegro**.</span></span>

    ![Creating an Azure AD test user](./media/abintegro-tutorial/tutorial_abintegro_search.png)

5. <span data-ttu-id="6a878-135">In the results panel, select **Abintegro**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="6a878-135">In the results panel, select **Abintegro**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/abintegro-tutorial/tutorial_abintegro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6a878-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6a878-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6a878-138">In this section, you configure and test Azure AD single sign-on with Abintegro based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="6a878-138">In this section, you configure and test Azure AD single sign-on with Abintegro based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6a878-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Abintegro is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a878-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Abintegro is to a user in Azure AD.</span></span> <span data-ttu-id="6a878-140">In other words, a link relationship between an Azure AD user and the related user in Abintegro needs to be established.</span><span class="sxs-lookup"><span data-stu-id="6a878-140">In other words, a link relationship between an Azure AD user and the related user in Abintegro needs to be established.</span></span>

<span data-ttu-id="6a878-141">In Abintegro, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="6a878-141">In Abintegro, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6a878-142">To configure and test Azure AD single sign-on with Abintegro, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6a878-142">To configure and test Azure AD single sign-on with Abintegro, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6a878-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="6a878-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6a878-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6a878-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6a878-145">**[Creating an Abintegro test user](#creating-an-abintegro-test-user)** - to have a counterpart of Britta Simon in Abintegro that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="6a878-145">**[Creating an Abintegro test user](#creating-an-abintegro-test-user)** - to have a counterpart of Britta Simon in Abintegro that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6a878-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6a878-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6a878-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="6a878-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6a878-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6a878-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6a878-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Abintegro application.</span><span class="sxs-lookup"><span data-stu-id="6a878-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Abintegro application.</span></span>

<span data-ttu-id="6a878-150">**To configure Azure AD single sign-on with Abintegro, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6a878-150">**To configure Azure AD single sign-on with Abintegro, perform the following steps:**</span></span>

1. <span data-ttu-id="6a878-151">In the Azure portal, on the **Abintegro** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6a878-151">In the Azure portal, on the **Abintegro** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="6a878-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6a878-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/abintegro-tutorial/tutorial_abintegro_samlbase.png)

3. <span data-ttu-id="6a878-155">On the **Abintegro Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6a878-155">On the **Abintegro Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/abintegro-tutorial/tutorial_abintegro_url.png)

    <span data-ttu-id="6a878-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span><span class="sxs-lookup"><span data-stu-id="6a878-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6a878-158">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="6a878-158">This value is not real.</span></span> <span data-ttu-id="6a878-159">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="6a878-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="6a878-160">Contact [Abintegro Client support team](mailto:support@abintegro.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="6a878-160">Contact [Abintegro Client support team](mailto:support@abintegro.com) to get this value.</span></span> 
 
4. <span data-ttu-id="6a878-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="6a878-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/abintegro-tutorial/tutorial_abintegro_certificate.png) 

5. <span data-ttu-id="6a878-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="6a878-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/abintegro-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6a878-165">To configure single sign-on on **Abintegro** side, you need to send the downloaded **Metadata XML** to [Abintegro support team](mailto:support@abintegro.com).</span><span class="sxs-lookup"><span data-stu-id="6a878-165">To configure single sign-on on **Abintegro** side, you need to send the downloaded **Metadata XML** to [Abintegro support team](mailto:support@abintegro.com).</span></span> <span data-ttu-id="6a878-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="6a878-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="6a878-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="6a878-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6a878-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="6a878-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6a878-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6a878-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6a878-170">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6a878-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="6a878-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6a878-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="6a878-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6a878-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6a878-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="6a878-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/abintegro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6a878-176">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="6a878-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/abintegro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6a878-178">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="6a878-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/abintegro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6a878-180">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6a878-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/abintegro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6a878-182">a.</span><span class="sxs-lookup"><span data-stu-id="6a878-182">a.</span></span> <span data-ttu-id="6a878-183">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6a878-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6a878-184">b.</span><span class="sxs-lookup"><span data-stu-id="6a878-184">b.</span></span> <span data-ttu-id="6a878-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6a878-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6a878-186">c.</span><span class="sxs-lookup"><span data-stu-id="6a878-186">c.</span></span> <span data-ttu-id="6a878-187">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="6a878-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6a878-188">d.</span><span class="sxs-lookup"><span data-stu-id="6a878-188">d.</span></span> <span data-ttu-id="6a878-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6a878-189">Click **Create**.</span></span>
 
### <a name="creating-an-abintegro-test-user"></a><span data-ttu-id="6a878-190">Creating an Abintegro test user</span><span class="sxs-lookup"><span data-stu-id="6a878-190">Creating an Abintegro test user</span></span>

<span data-ttu-id="6a878-191">There is no action item for you to configure user provisioning to Abintegro.</span><span class="sxs-lookup"><span data-stu-id="6a878-191">There is no action item for you to configure user provisioning to Abintegro.</span></span> <span data-ttu-id="6a878-192">When an assigned user tries to log into Abintegro using the access panel, Abintegro checks whether the user exists.</span><span class="sxs-lookup"><span data-stu-id="6a878-192">When an assigned user tries to log into Abintegro using the access panel, Abintegro checks whether the user exists.</span></span>
  
<span data-ttu-id="6a878-193">If there is no user account available yet, it is automatically created by Abintegro.</span><span class="sxs-lookup"><span data-stu-id="6a878-193">If there is no user account available yet, it is automatically created by Abintegro.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6a878-194">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6a878-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6a878-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Abintegro.</span><span class="sxs-lookup"><span data-stu-id="6a878-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Abintegro.</span></span>

![Assign User][200] 

<span data-ttu-id="6a878-197">**To assign Britta Simon to Abintegro, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6a878-197">**To assign Britta Simon to Abintegro, perform the following steps:**</span></span>

1. <span data-ttu-id="6a878-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6a878-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="6a878-200">In the applications list, select **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="6a878-200">In the applications list, select **Abintegro**.</span></span>

    ![Configure Single Sign-On](./media/abintegro-tutorial/tutorial_abintegro_app.png) 

3. <span data-ttu-id="6a878-202">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="6a878-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="6a878-204">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="6a878-204">Click **Add** button.</span></span> <span data-ttu-id="6a878-205">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6a878-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="6a878-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="6a878-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6a878-208">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="6a878-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6a878-209">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6a878-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6a878-210">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="6a878-210">Testing single sign-on</span></span>

<span data-ttu-id="6a878-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="6a878-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6a878-212">When you click the Abintegro tile in the Access Panel, you should get login page of Abintegro application.</span><span class="sxs-lookup"><span data-stu-id="6a878-212">When you click the Abintegro tile in the Access Panel, you should get login page of Abintegro application.</span></span>
<span data-ttu-id="6a878-213">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6a878-213">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6a878-214">Additional resources</span><span class="sxs-lookup"><span data-stu-id="6a878-214">Additional resources</span></span>

* [<span data-ttu-id="6a878-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a878-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="6a878-216">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6a878-216">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/abintegro-tutorial/tutorial_general_01.png
[2]: ./media/abintegro-tutorial/tutorial_general_02.png
[3]: ./media/abintegro-tutorial/tutorial_general_03.png
[4]: ./media/abintegro-tutorial/tutorial_general_04.png

[100]: ./media/abintegro-tutorial/tutorial_general_100.png

[200]: ./media/abintegro-tutorial/tutorial_general_200.png
[201]: ./media/abintegro-tutorial/tutorial_general_201.png
[202]: ./media/abintegro-tutorial/tutorial_general_202.png
[203]: ./media/abintegro-tutorial/tutorial_general_203.png

