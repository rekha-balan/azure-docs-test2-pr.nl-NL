---
title: 'Tutorial: Azure Active Directory integration with Optimizely | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Optimizely.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2018
ms.author: jeedes
ms.openlocfilehash: be56218e174e5d8b0e6bde394f2dfd40fc91e87d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969378"
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a><span data-ttu-id="a80ee-103">Tutorial: Azure Active Directory integration with Optimizely</span><span class="sxs-lookup"><span data-stu-id="a80ee-103">Tutorial: Azure Active Directory integration with Optimizely</span></span>

<span data-ttu-id="a80ee-104">In this tutorial, you learn how to integrate Optimizely with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a80ee-104">In this tutorial, you learn how to integrate Optimizely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a80ee-105">Integrating Optimizely with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a80ee-105">Integrating Optimizely with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a80ee-106">You can control in Azure AD who has access to Optimizely</span><span class="sxs-lookup"><span data-stu-id="a80ee-106">You can control in Azure AD who has access to Optimizely</span></span>
- <span data-ttu-id="a80ee-107">You can enable your users to automatically get signed-on to Optimizely (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="a80ee-107">You can enable your users to automatically get signed-on to Optimizely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a80ee-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a80ee-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a80ee-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a80ee-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a80ee-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a80ee-110">Prerequisites</span></span>

<span data-ttu-id="a80ee-111">To configure Azure AD integration with Optimizely, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a80ee-111">To configure Azure AD integration with Optimizely, you need the following items:</span></span>

- <span data-ttu-id="a80ee-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a80ee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a80ee-113">An Optimizely single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a80ee-113">An Optimizely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a80ee-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a80ee-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a80ee-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a80ee-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a80ee-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a80ee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a80ee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a80ee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a80ee-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a80ee-118">Scenario description</span></span>

<span data-ttu-id="a80ee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a80ee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="a80ee-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a80ee-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a80ee-121">Adding Optimizely from the gallery</span><span class="sxs-lookup"><span data-stu-id="a80ee-121">Adding Optimizely from the gallery</span></span>
2. <span data-ttu-id="a80ee-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a80ee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-optimizely-from-the-gallery"></a><span data-ttu-id="a80ee-123">Adding Optimizely from the gallery</span><span class="sxs-lookup"><span data-stu-id="a80ee-123">Adding Optimizely from the gallery</span></span>

<span data-ttu-id="a80ee-124">To configure the integration of Optimizely into Azure AD, you need to add Optimizely from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a80ee-124">To configure the integration of Optimizely into Azure AD, you need to add Optimizely from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a80ee-125">**To add Optimizely from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a80ee-125">**To add Optimizely from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a80ee-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a80ee-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a80ee-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a80ee-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a80ee-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a80ee-129">Then go to **All applications**.</span></span>

    ![Applications][2]

3. <span data-ttu-id="a80ee-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a80ee-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a80ee-133">In the search box, type **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="a80ee-133">In the search box, type **Optimizely**.</span></span>

    ![Creating an Azure AD test user](./media/optimizely-tutorial/tutorial_optimizely_search.png)

5. <span data-ttu-id="a80ee-135">In the results panel, select **Optimizely**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a80ee-135">In the results panel, select **Optimizely**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a80ee-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a80ee-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="a80ee-138">In this section, you configure and test Azure AD single sign-on with Optimizely based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a80ee-138">In this section, you configure and test Azure AD single sign-on with Optimizely based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a80ee-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Optimizely is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a80ee-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Optimizely is to a user in Azure AD.</span></span> <span data-ttu-id="a80ee-140">In other words, a link relationship between an Azure AD user and the related user in Optimizely needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a80ee-140">In other words, a link relationship between an Azure AD user and the related user in Optimizely needs to be established.</span></span>

<span data-ttu-id="a80ee-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Optimizely.</span><span class="sxs-lookup"><span data-stu-id="a80ee-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Optimizely.</span></span>

<span data-ttu-id="a80ee-142">To configure and test Azure AD single sign-on with Optimizely, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a80ee-142">To configure and test Azure AD single sign-on with Optimizely, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a80ee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a80ee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a80ee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a80ee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a80ee-145">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - to have a counterpart of Britta Simon in Optimizely that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a80ee-145">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - to have a counterpart of Britta Simon in Optimizely that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a80ee-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a80ee-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a80ee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a80ee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a80ee-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a80ee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a80ee-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Optimizely application.</span><span class="sxs-lookup"><span data-stu-id="a80ee-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Optimizely application.</span></span>

<span data-ttu-id="a80ee-150">**To configure Azure AD single sign-on with Optimizely, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a80ee-150">**To configure Azure AD single sign-on with Optimizely, perform the following steps:**</span></span>

1. <span data-ttu-id="a80ee-151">In the Azure portal, on the **Optimizely** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a80ee-151">In the Azure portal, on the **Optimizely** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="a80ee-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a80ee-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configure Single Sign-On](./media/optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. <span data-ttu-id="a80ee-155">On the **Optimizely Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a80ee-155">On the **Optimizely Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/optimizely-tutorial/tutorial_optimizely_url.png)

    <span data-ttu-id="a80ee-157">a.</span><span class="sxs-lookup"><span data-stu-id="a80ee-157">a.</span></span> <span data-ttu-id="a80ee-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.optimizely.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="a80ee-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.optimizely.net/<instance name>`</span></span>

    <span data-ttu-id="a80ee-159">b.</span><span class="sxs-lookup"><span data-stu-id="a80ee-159">b.</span></span> <span data-ttu-id="a80ee-160">In the **Identifier** textbox, type a URL using the following pattern:  `urn:auth0:optimizely:contoso`</span><span class="sxs-lookup"><span data-stu-id="a80ee-160">In the **Identifier** textbox, type a URL using the following pattern:  `urn:auth0:optimizely:contoso`</span></span>

    > [!NOTE]
    > <span data-ttu-id="a80ee-161">These values are not the real.</span><span class="sxs-lookup"><span data-stu-id="a80ee-161">These values are not the real.</span></span> <span data-ttu-id="a80ee-162">You will update the value with the actual Sign-on URL and Identifier, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="a80ee-162">You will update the value with the actual Sign-on URL and Identifier, which is explained later in the tutorial.</span></span>

4. <span data-ttu-id="a80ee-163">Optimizely application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="a80ee-163">Optimizely application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="a80ee-164">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="a80ee-164">Please configure the following claims for this application.</span></span> <span data-ttu-id="a80ee-165">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="a80ee-165">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="a80ee-166">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="a80ee-166">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On](./media/optimizely-tutorial/tutorial_optimizely_attribute.png)
    
5. <span data-ttu-id="a80ee-168">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span><span class="sxs-lookup"><span data-stu-id="a80ee-168">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="a80ee-169">Perform the following steps on each of the displayed attributes-</span><span class="sxs-lookup"><span data-stu-id="a80ee-169">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="a80ee-170">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="a80ee-170">Attribute Name</span></span> | <span data-ttu-id="a80ee-171">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="a80ee-171">Attribute Value</span></span> |
    | ---------------| --------------- |
    | <span data-ttu-id="a80ee-172">email</span><span class="sxs-lookup"><span data-stu-id="a80ee-172">email</span></span> | <span data-ttu-id="a80ee-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="a80ee-173">user.mail</span></span> |

    <span data-ttu-id="a80ee-174">a.</span><span class="sxs-lookup"><span data-stu-id="a80ee-174">a.</span></span> <span data-ttu-id="a80ee-175">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="a80ee-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/optimizely-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/optimizely-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="a80ee-178">b.</span><span class="sxs-lookup"><span data-stu-id="a80ee-178">b.</span></span> <span data-ttu-id="a80ee-179">In the **Name** textbox, type the **attribute name** shown for that row.</span><span class="sxs-lookup"><span data-stu-id="a80ee-179">In the **Name** textbox, type the **attribute name** shown for that row.</span></span>

    <span data-ttu-id="a80ee-180">c.</span><span class="sxs-lookup"><span data-stu-id="a80ee-180">c.</span></span> <span data-ttu-id="a80ee-181">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="a80ee-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="a80ee-182">d.</span><span class="sxs-lookup"><span data-stu-id="a80ee-182">d.</span></span> <span data-ttu-id="a80ee-183">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="a80ee-183">Click **Ok**.</span></span>

6. <span data-ttu-id="a80ee-184">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a80ee-184">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/optimizely-tutorial/tutorial_optimizely_certificate.png)

7. <span data-ttu-id="a80ee-186">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a80ee-186">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/optimizely-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a80ee-188">On the **Optimizely Configuration** section, click **Configure Optimizely** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="a80ee-188">On the **Optimizely Configuration** section, click **Configure Optimizely** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a80ee-189">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="a80ee-189">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/optimizely-tutorial/tutorial_optimizely_configure.png)

9. <span data-ttu-id="a80ee-191">To configure single sign-on on **Optimizely** side, contact your Optimizely Account Manager and provide the downloaded **Certificate (Base64)**, and **SAML Single Sign-On Service URL**.</span><span class="sxs-lookup"><span data-stu-id="a80ee-191">To configure single sign-on on **Optimizely** side, contact your Optimizely Account Manager and provide the downloaded **Certificate (Base64)**, and **SAML Single Sign-On Service URL**.</span></span>

10. <span data-ttu-id="a80ee-192">In response to your email, Optimizely provides you with the Sign On URL (SP-initiated SSO) and the Identifier (Service Provider Entity ID) values.</span><span class="sxs-lookup"><span data-stu-id="a80ee-192">In response to your email, Optimizely provides you with the Sign On URL (SP-initiated SSO) and the Identifier (Service Provider Entity ID) values.</span></span>

    <span data-ttu-id="a80ee-193">a.</span><span class="sxs-lookup"><span data-stu-id="a80ee-193">a.</span></span> <span data-ttu-id="a80ee-194">Copy the **SP-initiated SSO URL** provided by Optimizely, and paste into the **Sign On URL** textbox in **Optimizely Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a80ee-194">Copy the **SP-initiated SSO URL** provided by Optimizely, and paste into the **Sign On URL** textbox in **Optimizely Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="a80ee-195">b.</span><span class="sxs-lookup"><span data-stu-id="a80ee-195">b.</span></span> <span data-ttu-id="a80ee-196">Copy the **Service Provider Entity ID** provided by Optimizely, and paste into the **Identifier** textbox in **Optimizely Domain and URLs** section on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a80ee-196">Copy the **Service Provider Entity ID** provided by Optimizely, and paste into the **Identifier** textbox in **Optimizely Domain and URLs** section on Azure portal.</span></span>

11. <span data-ttu-id="a80ee-197">In a different browser window, sign-on to your Optimizely application.</span><span class="sxs-lookup"><span data-stu-id="a80ee-197">In a different browser window, sign-on to your Optimizely application.</span></span>

12. <span data-ttu-id="a80ee-198">Click you account name in the top right corner and then **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="a80ee-198">Click you account name in the top right corner and then **Account Settings**.</span></span>

    ![Azure AD Single Sign-On](./media/optimizely-tutorial/tutorial_optimizely_09.png)

13. <span data-ttu-id="a80ee-200">In the Account tab, check the box **Enable SSO** under Single Sign On in the **Overview** section.</span><span class="sxs-lookup"><span data-stu-id="a80ee-200">In the Account tab, check the box **Enable SSO** under Single Sign On in the **Overview** section.</span></span>
  
    ![Azure AD Single Sign-On](./media/optimizely-tutorial/tutorial_optimizely_10.png)

14. <span data-ttu-id="a80ee-202">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="a80ee-202">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a80ee-203">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a80ee-203">Creating an Azure AD test user</span></span>

<span data-ttu-id="a80ee-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a80ee-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="a80ee-206">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a80ee-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a80ee-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a80ee-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/optimizely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a80ee-209">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a80ee-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/optimizely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a80ee-211">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="a80ee-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/optimizely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a80ee-213">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a80ee-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/optimizely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a80ee-215">a.</span><span class="sxs-lookup"><span data-stu-id="a80ee-215">a.</span></span> <span data-ttu-id="a80ee-216">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a80ee-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a80ee-217">b.</span><span class="sxs-lookup"><span data-stu-id="a80ee-217">b.</span></span> <span data-ttu-id="a80ee-218">In the **User name** textbox, type the **email address** of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a80ee-218">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="a80ee-219">c.</span><span class="sxs-lookup"><span data-stu-id="a80ee-219">c.</span></span> <span data-ttu-id="a80ee-220">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="a80ee-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a80ee-221">d.</span><span class="sxs-lookup"><span data-stu-id="a80ee-221">d.</span></span> <span data-ttu-id="a80ee-222">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a80ee-222">Click **Create**.</span></span>

### <a name="creating-an-optimizely-test-user"></a><span data-ttu-id="a80ee-223">Creating an Optimizely test user</span><span class="sxs-lookup"><span data-stu-id="a80ee-223">Creating an Optimizely test user</span></span>

<span data-ttu-id="a80ee-224">In this section, you create a user called Britta Simon in Optimizely.</span><span class="sxs-lookup"><span data-stu-id="a80ee-224">In this section, you create a user called Britta Simon in Optimizely.</span></span>

1. <span data-ttu-id="a80ee-225">On the home page, select **Collaborators** tab.</span><span class="sxs-lookup"><span data-stu-id="a80ee-225">On the home page, select **Collaborators** tab.</span></span>

2. <span data-ttu-id="a80ee-226">To add new collaborator to the project, click **New Collaborator**.</span><span class="sxs-lookup"><span data-stu-id="a80ee-226">To add new collaborator to the project, click **New Collaborator**.</span></span>
   
    ![Creating an Azure AD test user](./media/optimizely-tutorial/create_aaduser_10.png)

3. <span data-ttu-id="a80ee-228">Fill in the email address and assign them a role.</span><span class="sxs-lookup"><span data-stu-id="a80ee-228">Fill in the email address and assign them a role.</span></span> <span data-ttu-id="a80ee-229">Click **Invite**.</span><span class="sxs-lookup"><span data-stu-id="a80ee-229">Click **Invite**.</span></span>

    ![Creating an Azure AD test user](./media/optimizely-tutorial/create_aaduser_11.png)

4. <span data-ttu-id="a80ee-231">They receive an email invite.</span><span class="sxs-lookup"><span data-stu-id="a80ee-231">They receive an email invite.</span></span> <span data-ttu-id="a80ee-232">Using the email address, they have to log in to Optimizely.</span><span class="sxs-lookup"><span data-stu-id="a80ee-232">Using the email address, they have to log in to Optimizely.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a80ee-233">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a80ee-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a80ee-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Optimizely.</span><span class="sxs-lookup"><span data-stu-id="a80ee-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Optimizely.</span></span>

![Assign User][200] 

<span data-ttu-id="a80ee-236">**To assign Britta Simon to Optimizely, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a80ee-236">**To assign Britta Simon to Optimizely, perform the following steps:**</span></span>

1. <span data-ttu-id="a80ee-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a80ee-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="a80ee-239">In the applications list, select **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="a80ee-239">In the applications list, select **Optimizely**.</span></span>

    ![Configure Single Sign-On](./media/optimizely-tutorial/tutorial_optimizely_app.png) 

3. <span data-ttu-id="a80ee-241">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a80ee-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202]

4. <span data-ttu-id="a80ee-243">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a80ee-243">Click **Add** button.</span></span> <span data-ttu-id="a80ee-244">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a80ee-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="a80ee-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a80ee-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a80ee-247">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a80ee-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a80ee-248">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a80ee-248">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="a80ee-249">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="a80ee-249">Testing single sign-on</span></span>

<span data-ttu-id="a80ee-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a80ee-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a80ee-251">When you click the Optimizely tile in the Access Panel, you should get automatically signed-on to your Optimizely application.</span><span class="sxs-lookup"><span data-stu-id="a80ee-251">When you click the Optimizely tile in the Access Panel, you should get automatically signed-on to your Optimizely application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a80ee-252">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a80ee-252">Additional resources</span></span>

* [<span data-ttu-id="a80ee-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a80ee-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a80ee-254">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a80ee-254">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/optimizely-tutorial/tutorial_general_01.png
[2]: ./media/optimizely-tutorial/tutorial_general_02.png
[3]: ./media/optimizely-tutorial/tutorial_general_03.png
[4]: ./media/optimizely-tutorial/tutorial_general_04.png

[100]: ./media/optimizely-tutorial/tutorial_general_100.png

[200]: ./media/optimizely-tutorial/tutorial_general_200.png
[201]: ./media/optimizely-tutorial/tutorial_general_201.png
[202]: ./media/optimizely-tutorial/tutorial_general_202.png
[203]: ./media/optimizely-tutorial/tutorial_general_203.png