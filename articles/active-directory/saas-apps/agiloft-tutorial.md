---
title: 'Tutorial: Azure Active Directory integration with Agiloft | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Agiloft.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: aca13814-cdbd-46b8-93dc-1578099c5ee4
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/09/2017
ms.author: jeedes
ms.openlocfilehash: f11d705cceb05c9e9cd0b340a680684eecf4f5d9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857478"
---
# <a name="tutorial-azure-active-directory-integration-with-agiloft"></a><span data-ttu-id="a1308-103">Tutorial: Azure Active Directory integration with Agiloft</span><span class="sxs-lookup"><span data-stu-id="a1308-103">Tutorial: Azure Active Directory integration with Agiloft</span></span>

<span data-ttu-id="a1308-104">In this tutorial, you learn how to integrate Agiloft with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a1308-104">In this tutorial, you learn how to integrate Agiloft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a1308-105">Integrating Agiloft with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a1308-105">Integrating Agiloft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a1308-106">You can control in Azure AD who has access to Agiloft.</span><span class="sxs-lookup"><span data-stu-id="a1308-106">You can control in Azure AD who has access to Agiloft.</span></span>
- <span data-ttu-id="a1308-107">You can enable your users to automatically get signed-on to Agiloft (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="a1308-107">You can enable your users to automatically get signed-on to Agiloft (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a1308-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a1308-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="a1308-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a1308-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1308-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a1308-110">Prerequisites</span></span>

<span data-ttu-id="a1308-111">To configure Azure AD integration with Agiloft, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a1308-111">To configure Azure AD integration with Agiloft, you need the following items:</span></span>

- <span data-ttu-id="a1308-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a1308-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a1308-113">An Agiloft single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a1308-113">An Agiloft single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a1308-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a1308-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a1308-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a1308-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a1308-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a1308-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a1308-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a1308-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a1308-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a1308-118">Scenario description</span></span>
<span data-ttu-id="a1308-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a1308-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a1308-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a1308-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a1308-121">Adding Agiloft from the gallery</span><span class="sxs-lookup"><span data-stu-id="a1308-121">Adding Agiloft from the gallery</span></span>
2. <span data-ttu-id="a1308-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a1308-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-agiloft-from-the-gallery"></a><span data-ttu-id="a1308-123">Adding Agiloft from the gallery</span><span class="sxs-lookup"><span data-stu-id="a1308-123">Adding Agiloft from the gallery</span></span>
<span data-ttu-id="a1308-124">To configure the integration of Agiloft into Azure AD, you need to add Agiloft from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a1308-124">To configure the integration of Agiloft into Azure AD, you need to add Agiloft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a1308-125">**To add Agiloft from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a1308-125">**To add Agiloft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a1308-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a1308-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="a1308-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a1308-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a1308-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a1308-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="a1308-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a1308-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="a1308-133">In the search box, type **Agiloft**, select **Agiloft** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a1308-133">In the search box, type **Agiloft**, select **Agiloft** from result panel then click **Add** button to add the application.</span></span>

    ![Agiloft in the results list](./media/agiloft-tutorial/tutorial_agiloft_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a1308-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a1308-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a1308-136">In this section, you configure and test Azure AD single sign-on with Agiloft based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a1308-136">In this section, you configure and test Azure AD single sign-on with Agiloft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a1308-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Agiloft is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1308-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Agiloft is to a user in Azure AD.</span></span> <span data-ttu-id="a1308-138">In other words, a link relationship between an Azure AD user and the related user in Agiloft needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a1308-138">In other words, a link relationship between an Azure AD user and the related user in Agiloft needs to be established.</span></span>

<span data-ttu-id="a1308-139">In Agiloft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="a1308-139">In Agiloft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a1308-140">To configure and test Azure AD single sign-on with Agiloft, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a1308-140">To configure and test Azure AD single sign-on with Agiloft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a1308-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a1308-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a1308-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a1308-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a1308-143">**[Create an Agiloft test user](#create-an-agiloft-test-user)** - to have a counterpart of Britta Simon in Agiloft that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a1308-143">**[Create an Agiloft test user](#create-an-agiloft-test-user)** - to have a counterpart of Britta Simon in Agiloft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a1308-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a1308-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a1308-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a1308-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a1308-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a1308-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a1308-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Agiloft application.</span><span class="sxs-lookup"><span data-stu-id="a1308-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Agiloft application.</span></span>

<span data-ttu-id="a1308-148">**To configure Azure AD single sign-on with Agiloft, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a1308-148">**To configure Azure AD single sign-on with Agiloft, perform the following steps:**</span></span>

1. <span data-ttu-id="a1308-149">In the Azure portal, on the **Agiloft** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a1308-149">In the Azure portal, on the **Agiloft** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="a1308-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a1308-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/agiloft-tutorial/tutorial_agiloft_samlbase.png)

3. <span data-ttu-id="a1308-153">On the **Agiloft Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span><span class="sxs-lookup"><span data-stu-id="a1308-153">On the **Agiloft Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Agiloft Domain and URLs single sign-on information](./media/agiloft-tutorial/tutorial_agiloft_url.png)

    <span data-ttu-id="a1308-155">a.</span><span class="sxs-lookup"><span data-stu-id="a1308-155">a.</span></span> <span data-ttu-id="a1308-156">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="a1308-156">In the **Identifier** textbox, type a URL using the following pattern:</span></span> 
    | |
    |-|-|
    | `https://<subdomain>.saas.enterprisewizard.com/project/<KB_NAME>` |
    | `https://<subdomain>.agiloft.com/project/<KB_NAME>` |

    <span data-ttu-id="a1308-157">b.</span><span class="sxs-lookup"><span data-stu-id="a1308-157">b.</span></span> <span data-ttu-id="a1308-158">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="a1308-158">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |-|-|
    | `https://<subdomain>.saas.enterprisewizard.com:443/gui2/spsamlsso?project=<KB_NAME>` |
    | `https://<subdomain>.agiloft.com:443/gui2/spsamlsso?project=<KB_NAME>` |

4. <span data-ttu-id="a1308-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="a1308-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Agiloft Domain and URLs single sign-on information](./media/agiloft-tutorial/tutorial_agiloft_url1.png)

    <span data-ttu-id="a1308-161">In the **Sign-on URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="a1308-161">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span> 
    | |
    |-|-|
    | `https://<subdomain>.saas.enterprisewizard.com/gui2/samlssologin.jsp?project=<KB_NAME>` |
    | `https://<subdomain>.agiloft.com/gui2/samlssologin.jsp?project=<KB_NAME>` |
     
    > [!NOTE] 
    > <span data-ttu-id="a1308-162">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="a1308-162">These values are not real.</span></span> <span data-ttu-id="a1308-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="a1308-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="a1308-164">Contact [Agiloft Client support team](https://www.agiloft.com/support-login.htm) to get these values.</span><span class="sxs-lookup"><span data-stu-id="a1308-164">Contact [Agiloft Client support team](https://www.agiloft.com/support-login.htm) to get these values.</span></span> 

5. <span data-ttu-id="a1308-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a1308-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/agiloft-tutorial/tutorial_agiloft_certificate.png) 

6. <span data-ttu-id="a1308-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a1308-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/agiloft-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="a1308-169">On the **Agiloft Configuration** section, click **Configure Agiloft** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="a1308-169">On the **Agiloft Configuration** section, click **Configure Agiloft** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a1308-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="a1308-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Agiloft Configuration](./media/agiloft-tutorial/tutorial_agiloft_configure.png) 

8. <span data-ttu-id="a1308-172">In a different web browser window, log in to your Agiloft company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a1308-172">In a different web browser window, log in to your Agiloft company site as an administrator.</span></span>

9. <span data-ttu-id="a1308-173">Click on **Setup** (on the Left Pane) and then **Access**.</span><span class="sxs-lookup"><span data-stu-id="a1308-173">Click on **Setup** (on the Left Pane) and then **Access**.</span></span>

    ![Agiloft Configuration](./media/agiloft-tutorial/setup1.png) 

10. <span data-ttu-id="a1308-175">Click on   the button **“Configure SAML 2.0 Single Sign-On“**.</span><span class="sxs-lookup"><span data-stu-id="a1308-175">Click on   the button **“Configure SAML 2.0 Single Sign-On“**.</span></span> 
    
    ![Agiloft Configuration](./media/agiloft-tutorial/setup2.png) 

11. <span data-ttu-id="a1308-177">A wizard dialog appears.</span><span class="sxs-lookup"><span data-stu-id="a1308-177">A wizard dialog appears.</span></span> <span data-ttu-id="a1308-178">On the dialog, click on the TAB  **“Identity Provider Details”** and fill in the following fields:</span><span class="sxs-lookup"><span data-stu-id="a1308-178">On the dialog, click on the TAB  **“Identity Provider Details”** and fill in the following fields:</span></span>  
    
    ![Agiloft Configuration](./media/agiloft-tutorial/setup4.png) 

    <span data-ttu-id="a1308-180">a.</span><span class="sxs-lookup"><span data-stu-id="a1308-180">a.</span></span> <span data-ttu-id="a1308-181">In **IdP Entity Id / Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a1308-181">In **IdP Entity Id / Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a1308-182">b.</span><span class="sxs-lookup"><span data-stu-id="a1308-182">b.</span></span> <span data-ttu-id="a1308-183">In **IdP Login URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a1308-183">In **IdP Login URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a1308-184">c.</span><span class="sxs-lookup"><span data-stu-id="a1308-184">c.</span></span> <span data-ttu-id="a1308-185">In **IdP Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a1308-185">In **IdP Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a1308-186">d.</span><span class="sxs-lookup"><span data-stu-id="a1308-186">d.</span></span> <span data-ttu-id="a1308-187">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **IdP Provided X.509 certificate contents** textbox.</span><span class="sxs-lookup"><span data-stu-id="a1308-187">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **IdP Provided X.509 certificate contents** textbox.</span></span>

    <span data-ttu-id="a1308-188">e.</span><span class="sxs-lookup"><span data-stu-id="a1308-188">e.</span></span> <span data-ttu-id="a1308-189">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="a1308-189">Click **Finish**.</span></span>


> [!TIP]
> <span data-ttu-id="a1308-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="a1308-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a1308-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="a1308-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a1308-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a1308-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a1308-193">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a1308-193">Create an Azure AD test user</span></span>

<span data-ttu-id="a1308-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a1308-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="a1308-196">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a1308-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a1308-197">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="a1308-197">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/agiloft-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a1308-199">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a1308-199">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/agiloft-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a1308-201">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="a1308-201">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/agiloft-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a1308-203">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a1308-203">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/agiloft-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a1308-205">a.</span><span class="sxs-lookup"><span data-stu-id="a1308-205">a.</span></span> <span data-ttu-id="a1308-206">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a1308-206">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a1308-207">b.</span><span class="sxs-lookup"><span data-stu-id="a1308-207">b.</span></span> <span data-ttu-id="a1308-208">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a1308-208">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="a1308-209">c.</span><span class="sxs-lookup"><span data-stu-id="a1308-209">c.</span></span> <span data-ttu-id="a1308-210">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="a1308-210">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="a1308-211">d.</span><span class="sxs-lookup"><span data-stu-id="a1308-211">d.</span></span> <span data-ttu-id="a1308-212">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a1308-212">Click **Create**.</span></span>
 
### <a name="create-an-agiloft-test-user"></a><span data-ttu-id="a1308-213">Create an Agiloft test user</span><span class="sxs-lookup"><span data-stu-id="a1308-213">Create an Agiloft test user</span></span>

<span data-ttu-id="a1308-214">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span><span class="sxs-lookup"><span data-stu-id="a1308-214">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="a1308-215">There is no action for you in this section.</span><span class="sxs-lookup"><span data-stu-id="a1308-215">There is no action for you in this section.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a1308-216">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a1308-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="a1308-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Agiloft.</span><span class="sxs-lookup"><span data-stu-id="a1308-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Agiloft.</span></span>

![Assign the user role][200] 

<span data-ttu-id="a1308-219">**To assign Britta Simon to Agiloft, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a1308-219">**To assign Britta Simon to Agiloft, perform the following steps:**</span></span>

1. <span data-ttu-id="a1308-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a1308-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="a1308-222">In the applications list, select **Agiloft**.</span><span class="sxs-lookup"><span data-stu-id="a1308-222">In the applications list, select **Agiloft**.</span></span>

    ![The Agiloft link in the Applications list](./media/agiloft-tutorial/tutorial_agiloft_app.png)  

3. <span data-ttu-id="a1308-224">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a1308-224">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="a1308-226">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a1308-226">Click **Add** button.</span></span> <span data-ttu-id="a1308-227">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a1308-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="a1308-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a1308-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a1308-230">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a1308-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a1308-231">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a1308-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a1308-232">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="a1308-232">Test single sign-on</span></span>

<span data-ttu-id="a1308-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a1308-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a1308-234">When you click the Agiloft tile in the Access Panel, you should get automatically signed-on to your Agiloft application.</span><span class="sxs-lookup"><span data-stu-id="a1308-234">When you click the Agiloft tile in the Access Panel, you should get automatically signed-on to your Agiloft application.</span></span>
<span data-ttu-id="a1308-235">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a1308-235">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a1308-236">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a1308-236">Additional resources</span></span>

* [<span data-ttu-id="a1308-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a1308-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a1308-238">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a1308-238">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/agiloft-tutorial/tutorial_general_01.png
[2]: ./media/agiloft-tutorial/tutorial_general_02.png
[3]: ./media/agiloft-tutorial/tutorial_general_03.png
[4]: ./media/agiloft-tutorial/tutorial_general_04.png

[100]: ./media/agiloft-tutorial/tutorial_general_100.png

[200]: ./media/agiloft-tutorial/tutorial_general_200.png
[201]: ./media/agiloft-tutorial/tutorial_general_201.png
[202]: ./media/agiloft-tutorial/tutorial_general_202.png
[203]: ./media/agiloft-tutorial/tutorial_general_203.png

