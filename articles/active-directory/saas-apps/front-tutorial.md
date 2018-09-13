---
title: 'Tutorial: Azure Active Directory integration with Front | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Front.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/15/2017
ms.author: jeedes
ms.openlocfilehash: d0bdf3ff282152f92e1b661bf19768489d1a029b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965536"
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="7f1e5-103">Tutorial: Azure Active Directory integration with Front</span><span class="sxs-lookup"><span data-stu-id="7f1e5-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="7f1e5-104">In this tutorial, you learn how to integrate Front with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7f1e5-104">In this tutorial, you learn how to integrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7f1e5-105">Integrating Front with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7f1e5-105">Integrating Front with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7f1e5-106">You can control in Azure AD who has access to Front.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-106">You can control in Azure AD who has access to Front.</span></span>
- <span data-ttu-id="7f1e5-107">You can enable your users to automatically get signed-on to Front (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-107">You can enable your users to automatically get signed-on to Front (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7f1e5-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="7f1e5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="7f1e5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f1e5-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7f1e5-110">Prerequisites</span></span>

<span data-ttu-id="7f1e5-111">To configure Azure AD integration with Front, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7f1e5-111">To configure Azure AD integration with Front, you need the following items:</span></span>

- <span data-ttu-id="7f1e5-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7f1e5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7f1e5-113">A Front single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7f1e5-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7f1e5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7f1e5-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7f1e5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7f1e5-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7f1e5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7f1e5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7f1e5-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7f1e5-118">Scenario description</span></span>
<span data-ttu-id="7f1e5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7f1e5-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7f1e5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7f1e5-121">Adding Front from the gallery</span><span class="sxs-lookup"><span data-stu-id="7f1e5-121">Adding Front from the gallery</span></span>
1. <span data-ttu-id="7f1e5-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7f1e5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-the-gallery"></a><span data-ttu-id="7f1e5-123">Adding Front from the gallery</span><span class="sxs-lookup"><span data-stu-id="7f1e5-123">Adding Front from the gallery</span></span>
<span data-ttu-id="7f1e5-124">To configure the integration of Front into Azure AD, you need to add Front from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-124">To configure the integration of Front into Azure AD, you need to add Front from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7f1e5-125">**To add Front from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7f1e5-125">**To add Front from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7f1e5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="7f1e5-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7f1e5-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="7f1e5-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="7f1e5-133">In the search box, type **Front**, select **Front** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-133">In the search box, type **Front**, select **Front** from result panel then click **Add** button to add the application.</span></span>

    ![Front in the results list](./media/front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7f1e5-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7f1e5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7f1e5-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7f1e5-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7f1e5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Front is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Front is to a user in Azure AD.</span></span> <span data-ttu-id="7f1e5-138">In other words, a link relationship between an Azure AD user and the related user in Front needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-138">In other words, a link relationship between an Azure AD user and the related user in Front needs to be established.</span></span>

<span data-ttu-id="7f1e5-139">In Front, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-139">In Front, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7f1e5-140">To configure and test Azure AD single sign-on with Front, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7f1e5-140">To configure and test Azure AD single sign-on with Front, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7f1e5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="7f1e5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="7f1e5-143">**[Create a Front test user](#create-a-front-test-user)** - to have a counterpart of Britta Simon in Front that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-143">**[Create a Front test user](#create-a-front-test-user)** - to have a counterpart of Britta Simon in Front that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="7f1e5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="7f1e5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7f1e5-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7f1e5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7f1e5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Front application.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="7f1e5-148">**To configure Azure AD single sign-on with Front, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7f1e5-148">**To configure Azure AD single sign-on with Front, perform the following steps:**</span></span>

1. <span data-ttu-id="7f1e5-149">In the Azure portal, on the **Front** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-149">In the Azure portal, on the **Front** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="7f1e5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/front-tutorial/tutorial_front_samlbase.png)

1. <span data-ttu-id="7f1e5-153">On the **Front Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7f1e5-153">On the **Front Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="7f1e5-155">a.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-155">a.</span></span> <span data-ttu-id="7f1e5-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="7f1e5-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="7f1e5-157">b.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-157">b.</span></span> <span data-ttu-id="7f1e5-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="7f1e5-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="7f1e5-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-159">These values are not real.</span></span> <span data-ttu-id="7f1e5-160">Update these values with the actual Identifier and Reply URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-160">Update these values with the actual Identifier and Reply URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) to get these values.</span></span> 

1. <span data-ttu-id="7f1e5-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/front-tutorial/tutorial_front_certificate.png) 

1. <span data-ttu-id="7f1e5-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/front-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="7f1e5-165">On the **Front Configuration** section, click **Configure Front** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-165">On the **Front Configuration** section, click **Configure Front** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7f1e5-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="7f1e5-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/front-tutorial/tutorial_front_configure.png) 

1. <span data-ttu-id="7f1e5-168">Sign-on to your Front tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-168">Sign-on to your Front tenant as an administrator.</span></span>

1. <span data-ttu-id="7f1e5-169">Go to **Settings (cog icon at the bottom of the left sidebar) > Preferences**.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-169">Go to **Settings (cog icon at the bottom of the left sidebar) > Preferences**.</span></span>
   
    ![Configure Single Sign-On On App side](./media/front-tutorial/tutorial_front_000.png)

1. <span data-ttu-id="7f1e5-171">Click **Single Sign On** link.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-171">Click **Single Sign On** link.</span></span>
   
    ![Configure Single Sign-On On App side](./media/front-tutorial/tutorial_front_001.png)

1. <span data-ttu-id="7f1e5-173">Select **SAML** in the drop-down list of **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-173">Select **SAML** in the drop-down list of **Single Sign On**.</span></span>
   
    ![Configure Single Sign-On On App side](./media/front-tutorial/tutorial_front_002.png)

1. <span data-ttu-id="7f1e5-175">In the **Entry Point** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-175">In the **Entry Point** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![Configure Single Sign-On On App side](./media/front-tutorial/tutorial_front_003.png)

1. <span data-ttu-id="7f1e5-177">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Signing certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-177">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Signing certificate** textbox.</span></span>
    
    ![Configure Single Sign-On On App side](./media/front-tutorial/tutorial_front_004.png)

1. <span data-ttu-id="7f1e5-179">On the **Service provider settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7f1e5-179">On the **Service provider settings** section, perform the following steps:</span></span>

    ![Configure Single Sign-On On App side](./media/front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="7f1e5-181">a.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-181">a.</span></span> <span data-ttu-id="7f1e5-182">Copy the value of **Entity ID** and paste it into the **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-182">Copy the value of **Entity ID** and paste it into the **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="7f1e5-183">b.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-183">b.</span></span> <span data-ttu-id="7f1e5-184">Copy the value of **ACS URL** and paste it into the **Reply URL** textbox in **Front Domain and URLs** section in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-184">Copy the value of **ACS URL** and paste it into the **Reply URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
1. <span data-ttu-id="7f1e5-185">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-185">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="7f1e5-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="7f1e5-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7f1e5-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7f1e5-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7f1e5-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7f1e5-189">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7f1e5-189">Create an Azure AD test user</span></span>

<span data-ttu-id="7f1e5-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="7f1e5-192">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7f1e5-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7f1e5-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/front-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="7f1e5-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/front-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="7f1e5-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/front-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="7f1e5-199">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7f1e5-199">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7f1e5-201">a.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-201">a.</span></span> <span data-ttu-id="7f1e5-202">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-202">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7f1e5-203">b.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-203">b.</span></span> <span data-ttu-id="7f1e5-204">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-204">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="7f1e5-205">c.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-205">c.</span></span> <span data-ttu-id="7f1e5-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="7f1e5-207">d.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-207">d.</span></span> <span data-ttu-id="7f1e5-208">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-208">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="7f1e5-209">Create a Front test user</span><span class="sxs-lookup"><span data-stu-id="7f1e5-209">Create a Front test user</span></span>

<span data-ttu-id="7f1e5-210">In this section, you create a user called Britta Simon in Front.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-210">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="7f1e5-211">Work with [Front Client support team](mailto:support@frontapp.com) to add the users in the Front platform.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-211">Work with [Front Client support team](mailto:support@frontapp.com) to add the users in the Front platform.</span></span> <span data-ttu-id="7f1e5-212">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-212">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7f1e5-213">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7f1e5-213">Assign the Azure AD test user</span></span>

<span data-ttu-id="7f1e5-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Front.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Front.</span></span>

![Assign the user role][200] 

<span data-ttu-id="7f1e5-216">**To assign Britta Simon to Front, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7f1e5-216">**To assign Britta Simon to Front, perform the following steps:**</span></span>

1. <span data-ttu-id="7f1e5-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="7f1e5-219">In the applications list, select **Front**.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-219">In the applications list, select **Front**.</span></span>

    ![The Front link in the Applications list](./media/front-tutorial/tutorial_front_app.png)  

1. <span data-ttu-id="7f1e5-221">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-221">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="7f1e5-223">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-223">Click **Add** button.</span></span> <span data-ttu-id="7f1e5-224">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="7f1e5-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="7f1e5-227">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-227">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="7f1e5-228">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7f1e5-229">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="7f1e5-229">Test single sign-on</span></span>

<span data-ttu-id="7f1e5-230">The objective of this section is to test your Azure AD SSOconfiguration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-230">The objective of this section is to test your Azure AD SSOconfiguration using the Access Panel.</span></span>

<span data-ttu-id="7f1e5-231">When you click the Front tile in the Access Panel, you should get automatically signed-on to your Front application.</span><span class="sxs-lookup"><span data-stu-id="7f1e5-231">When you click the Front tile in the Access Panel, you should get automatically signed-on to your Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7f1e5-232">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7f1e5-232">Additional resources</span></span>

* [<span data-ttu-id="7f1e5-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f1e5-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="7f1e5-234">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7f1e5-234">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/front-tutorial/tutorial_general_01.png
[2]: ./media/front-tutorial/tutorial_general_02.png
[3]: ./media/front-tutorial/tutorial_general_03.png
[4]: ./media/front-tutorial/tutorial_general_04.png

[100]: ./media/front-tutorial/tutorial_general_100.png

[200]: ./media/front-tutorial/tutorial_general_200.png
[201]: ./media/front-tutorial/tutorial_general_201.png
[202]: ./media/front-tutorial/tutorial_general_202.png
[203]: ./media/front-tutorial/tutorial_general_203.png

