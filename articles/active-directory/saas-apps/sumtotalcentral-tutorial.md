---
title: 'Tutorial: Azure Active Directory integration with SumTotalCentral | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SumTotalCentral.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 93ad629a-f516-4cac-bfe2-a77257e3a797
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/12/2017
ms.author: jeedes
ms.openlocfilehash: 1c604eebb2c1c85de717217063333190ffa865f4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867974"
---
# <a name="tutorial-azure-active-directory-integration-with-sumtotalcentral"></a><span data-ttu-id="abff2-103">Tutorial: Azure Active Directory integration with SumTotalCentral</span><span class="sxs-lookup"><span data-stu-id="abff2-103">Tutorial: Azure Active Directory integration with SumTotalCentral</span></span>

<span data-ttu-id="abff2-104">In this tutorial, you learn how to integrate SumTotalCentral with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="abff2-104">In this tutorial, you learn how to integrate SumTotalCentral with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="abff2-105">Integrating SumTotalCentral with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="abff2-105">Integrating SumTotalCentral with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="abff2-106">You can control in Azure AD who has access to SumTotalCentral.</span><span class="sxs-lookup"><span data-stu-id="abff2-106">You can control in Azure AD who has access to SumTotalCentral.</span></span>
- <span data-ttu-id="abff2-107">You can enable your users to automatically get signed-on to SumTotalCentral (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="abff2-107">You can enable your users to automatically get signed-on to SumTotalCentral (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="abff2-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="abff2-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="abff2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="abff2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abff2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="abff2-110">Prerequisites</span></span>

<span data-ttu-id="abff2-111">To configure Azure AD integration with SumTotalCentral, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="abff2-111">To configure Azure AD integration with SumTotalCentral, you need the following items:</span></span>

- <span data-ttu-id="abff2-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="abff2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="abff2-113">A SumTotalCentral single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="abff2-113">A SumTotalCentral single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="abff2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="abff2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="abff2-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="abff2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="abff2-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="abff2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="abff2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="abff2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="abff2-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="abff2-118">Scenario description</span></span>
<span data-ttu-id="abff2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="abff2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="abff2-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="abff2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="abff2-121">Adding SumTotalCentral from the gallery</span><span class="sxs-lookup"><span data-stu-id="abff2-121">Adding SumTotalCentral from the gallery</span></span>
1. <span data-ttu-id="abff2-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="abff2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sumtotalcentral-from-the-gallery"></a><span data-ttu-id="abff2-123">Adding SumTotalCentral from the gallery</span><span class="sxs-lookup"><span data-stu-id="abff2-123">Adding SumTotalCentral from the gallery</span></span>
<span data-ttu-id="abff2-124">To configure the integration of SumTotalCentral into Azure AD, you need to add SumTotalCentral from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="abff2-124">To configure the integration of SumTotalCentral into Azure AD, you need to add SumTotalCentral from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="abff2-125">**To add SumTotalCentral from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="abff2-125">**To add SumTotalCentral from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="abff2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="abff2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="abff2-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="abff2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="abff2-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="abff2-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="abff2-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="abff2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="abff2-133">In the search box, type **SumTotalCentral**, select **SumTotalCentral** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="abff2-133">In the search box, type **SumTotalCentral**, select **SumTotalCentral** from result panel then click **Add** button to add the application.</span></span>

    ![SumTotalCentral in the results list](./media/sumtotalcentral-tutorial/tutorial_sumtotalcentral_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="abff2-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="abff2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="abff2-136">In this section, you configure and test Azure AD single sign-on with SumTotalCentral based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="abff2-136">In this section, you configure and test Azure AD single sign-on with SumTotalCentral based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="abff2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SumTotalCentral is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="abff2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SumTotalCentral is to a user in Azure AD.</span></span> <span data-ttu-id="abff2-138">In other words, a link relationship between an Azure AD user and the related user in SumTotalCentral needs to be established.</span><span class="sxs-lookup"><span data-stu-id="abff2-138">In other words, a link relationship between an Azure AD user and the related user in SumTotalCentral needs to be established.</span></span>

<span data-ttu-id="abff2-139">In SumTotalCentral, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="abff2-139">In SumTotalCentral, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="abff2-140">To configure and test Azure AD single sign-on with SumTotalCentral, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="abff2-140">To configure and test Azure AD single sign-on with SumTotalCentral, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="abff2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="abff2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="abff2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="abff2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="abff2-143">**[Create a SumTotalCentral test user](#create-a-sumtotalcentral-test-user)** - to have a counterpart of Britta Simon in SumTotalCentral that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="abff2-143">**[Create a SumTotalCentral test user](#create-a-sumtotalcentral-test-user)** - to have a counterpart of Britta Simon in SumTotalCentral that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="abff2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="abff2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="abff2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="abff2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="abff2-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="abff2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="abff2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SumTotalCentral application.</span><span class="sxs-lookup"><span data-stu-id="abff2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SumTotalCentral application.</span></span>

<span data-ttu-id="abff2-148">**To configure Azure AD single sign-on with SumTotalCentral, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="abff2-148">**To configure Azure AD single sign-on with SumTotalCentral, perform the following steps:**</span></span>

1. <span data-ttu-id="abff2-149">In the Azure portal, on the **SumTotalCentral** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="abff2-149">In the Azure portal, on the **SumTotalCentral** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="abff2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="abff2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/sumtotalcentral-tutorial/tutorial_sumtotalcentral_samlbase.png)

1. <span data-ttu-id="abff2-153">On the **SumTotalCentral Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="abff2-153">On the **SumTotalCentral Domain and URLs** section, perform the following steps:</span></span>

    ![SumTotalCentral Domain and URLs single sign-on information](./media/sumtotalcentral-tutorial/tutorial_sumtotalcentral_url.png)

    <span data-ttu-id="abff2-155">a.</span><span class="sxs-lookup"><span data-stu-id="abff2-155">a.</span></span> <span data-ttu-id="abff2-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sumtotalsystems.com/sites/default`</span><span class="sxs-lookup"><span data-stu-id="abff2-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sumtotalsystems.com/sites/default`</span></span>

    <span data-ttu-id="abff2-157">b.</span><span class="sxs-lookup"><span data-stu-id="abff2-157">b.</span></span> <span data-ttu-id="abff2-158">In the **Identifier** textbox, type a value: `SumTotalFederationGateway`</span><span class="sxs-lookup"><span data-stu-id="abff2-158">In the **Identifier** textbox, type a value: `SumTotalFederationGateway`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="abff2-159">The Sign-on URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="abff2-159">The Sign-on URL value is not real.</span></span> <span data-ttu-id="abff2-160">Update the value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="abff2-160">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="abff2-161">Contact [SumTotalCentral Client support team](http://www.sumtotalsystems.com/support/) to get the value.</span><span class="sxs-lookup"><span data-stu-id="abff2-161">Contact [SumTotalCentral Client support team](http://www.sumtotalsystems.com/support/) to get the value.</span></span> 
 
1. <span data-ttu-id="abff2-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="abff2-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/sumtotalcentral-tutorial/tutorial_sumtotalcentral_certificate.png) 

1. <span data-ttu-id="abff2-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="abff2-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/sumtotalcentral-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="abff2-166">To configure single sign-on on **SumTotalCentral** side, you need to send the downloaded **Metadata XML** to [SumTotalCentral support team](http://www.sumtotalsystems.com/support/).</span><span class="sxs-lookup"><span data-stu-id="abff2-166">To configure single sign-on on **SumTotalCentral** side, you need to send the downloaded **Metadata XML** to [SumTotalCentral support team](http://www.sumtotalsystems.com/support/).</span></span> <span data-ttu-id="abff2-167">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="abff2-167">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="abff2-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="abff2-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="abff2-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="abff2-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="abff2-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="abff2-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="abff2-171">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="abff2-171">Create an Azure AD test user</span></span>

<span data-ttu-id="abff2-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="abff2-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="abff2-174">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="abff2-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="abff2-175">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="abff2-175">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/sumtotalcentral-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="abff2-177">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="abff2-177">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/sumtotalcentral-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="abff2-179">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="abff2-179">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/sumtotalcentral-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="abff2-181">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="abff2-181">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/sumtotalcentral-tutorial/create_aaduser_04.png)

    <span data-ttu-id="abff2-183">a.</span><span class="sxs-lookup"><span data-stu-id="abff2-183">a.</span></span> <span data-ttu-id="abff2-184">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="abff2-184">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="abff2-185">b.</span><span class="sxs-lookup"><span data-stu-id="abff2-185">b.</span></span> <span data-ttu-id="abff2-186">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="abff2-186">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="abff2-187">c.</span><span class="sxs-lookup"><span data-stu-id="abff2-187">c.</span></span> <span data-ttu-id="abff2-188">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="abff2-188">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="abff2-189">d.</span><span class="sxs-lookup"><span data-stu-id="abff2-189">d.</span></span> <span data-ttu-id="abff2-190">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="abff2-190">Click **Create**.</span></span>
 
### <a name="create-a-sumtotalcentral-test-user"></a><span data-ttu-id="abff2-191">Create a SumTotalCentral test user</span><span class="sxs-lookup"><span data-stu-id="abff2-191">Create a SumTotalCentral test user</span></span>

<span data-ttu-id="abff2-192">In this section, you create a user called Britta Simon in SumTotalCentral.</span><span class="sxs-lookup"><span data-stu-id="abff2-192">In this section, you create a user called Britta Simon in SumTotalCentral.</span></span> <span data-ttu-id="abff2-193">Work with [SumTotalCentral support team](http://www.sumtotalsystems.com/support/) to add the users in the SumTotalCentral platform.</span><span class="sxs-lookup"><span data-stu-id="abff2-193">Work with [SumTotalCentral support team](http://www.sumtotalsystems.com/support/) to add the users in the SumTotalCentral platform.</span></span> <span data-ttu-id="abff2-194">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="abff2-194">Users must be created and activated before you use single sign-on.</span></span>  

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="abff2-195">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="abff2-195">Assign the Azure AD test user</span></span>

<span data-ttu-id="abff2-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SumTotalCentral.</span><span class="sxs-lookup"><span data-stu-id="abff2-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SumTotalCentral.</span></span>

![Assign the user role][200] 

<span data-ttu-id="abff2-198">**To assign Britta Simon to SumTotalCentral, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="abff2-198">**To assign Britta Simon to SumTotalCentral, perform the following steps:**</span></span>

1. <span data-ttu-id="abff2-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="abff2-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="abff2-201">In the applications list, select **SumTotalCentral**.</span><span class="sxs-lookup"><span data-stu-id="abff2-201">In the applications list, select **SumTotalCentral**.</span></span>

    ![The SumTotalCentral link in the Applications list](./media/sumtotalcentral-tutorial/tutorial_sumtotalcentral_app.png)  

1. <span data-ttu-id="abff2-203">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="abff2-203">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="abff2-205">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="abff2-205">Click **Add** button.</span></span> <span data-ttu-id="abff2-206">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="abff2-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="abff2-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="abff2-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="abff2-209">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="abff2-209">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="abff2-210">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="abff2-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="abff2-211">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="abff2-211">Test single sign-on</span></span>

<span data-ttu-id="abff2-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="abff2-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="abff2-213">When you click the SumTotalCentral tile in the Access Panel, you should get automatically signed-on to your SumTotalCentral application.</span><span class="sxs-lookup"><span data-stu-id="abff2-213">When you click the SumTotalCentral tile in the Access Panel, you should get automatically signed-on to your SumTotalCentral application.</span></span>
<span data-ttu-id="abff2-214">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="abff2-214">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="abff2-215">Additional resources</span><span class="sxs-lookup"><span data-stu-id="abff2-215">Additional resources</span></span>

* [<span data-ttu-id="abff2-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="abff2-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="abff2-217">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="abff2-217">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/sumtotalcentral-tutorial/tutorial_general_01.png
[2]: ./media/sumtotalcentral-tutorial/tutorial_general_02.png
[3]: ./media/sumtotalcentral-tutorial/tutorial_general_03.png
[4]: ./media/sumtotalcentral-tutorial/tutorial_general_04.png

[100]: ./media/sumtotalcentral-tutorial/tutorial_general_100.png

[200]: ./media/sumtotalcentral-tutorial/tutorial_general_200.png
[201]: ./media/sumtotalcentral-tutorial/tutorial_general_201.png
[202]: ./media/sumtotalcentral-tutorial/tutorial_general_202.png
[203]: ./media/sumtotalcentral-tutorial/tutorial_general_203.png

