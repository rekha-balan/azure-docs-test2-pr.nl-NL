---
title: 'Tutorial: Azure Active Directory integration with Weekdone | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Weekdone.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 34921f9a-5637-4420-ab4c-9beb34421909
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2018
ms.author: jeedes
ms.openlocfilehash: 7f7946ece91013696969dafda17b02c972f4b780
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857789"
---
# <a name="tutorial-azure-active-directory-integration-with-weekdone"></a><span data-ttu-id="7c223-103">Tutorial: Azure Active Directory integration with Weekdone</span><span class="sxs-lookup"><span data-stu-id="7c223-103">Tutorial: Azure Active Directory integration with Weekdone</span></span>

<span data-ttu-id="7c223-104">In this tutorial, you learn how to integrate Weekdone with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7c223-104">In this tutorial, you learn how to integrate Weekdone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7c223-105">Integrating Weekdone with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7c223-105">Integrating Weekdone with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7c223-106">You can control in Azure AD who has access to Weekdone</span><span class="sxs-lookup"><span data-stu-id="7c223-106">You can control in Azure AD who has access to Weekdone</span></span>
- <span data-ttu-id="7c223-107">You can enable your users to automatically get signed-on to Weekdone (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="7c223-107">You can enable your users to automatically get signed-on to Weekdone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7c223-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7c223-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7c223-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="7c223-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c223-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7c223-110">Prerequisites</span></span>

<span data-ttu-id="7c223-111">To configure Azure AD integration with Weekdone, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7c223-111">To configure Azure AD integration with Weekdone, you need the following items:</span></span>

- <span data-ttu-id="7c223-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7c223-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7c223-113">A Weekdone single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7c223-113">A Weekdone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7c223-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7c223-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7c223-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7c223-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7c223-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="7c223-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7c223-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7c223-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7c223-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7c223-118">Scenario description</span></span>
<span data-ttu-id="7c223-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7c223-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7c223-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7c223-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7c223-121">Adding Weekdone from the gallery</span><span class="sxs-lookup"><span data-stu-id="7c223-121">Adding Weekdone from the gallery</span></span>
2. <span data-ttu-id="7c223-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7c223-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-weekdone-from-the-gallery"></a><span data-ttu-id="7c223-123">Adding Weekdone from the gallery</span><span class="sxs-lookup"><span data-stu-id="7c223-123">Adding Weekdone from the gallery</span></span>
<span data-ttu-id="7c223-124">To configure the integration of Weekdone into Azure AD, you need to add Weekdone from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7c223-124">To configure the integration of Weekdone into Azure AD, you need to add Weekdone from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7c223-125">**To add Weekdone from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7c223-125">**To add Weekdone from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7c223-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7c223-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7c223-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="7c223-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7c223-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7c223-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="7c223-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="7c223-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="7c223-133">In the search box, type **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="7c223-133">In the search box, type **Weekdone**.</span></span>

    ![Creating an Azure AD test user](./media/weekdone-tutorial/tutorial_weekdone_search.png)

5. <span data-ttu-id="7c223-135">In the results panel, select **Weekdone**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="7c223-135">In the results panel, select **Weekdone**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/weekdone-tutorial/tutorial_weekdone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7c223-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7c223-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7c223-138">In this section, you configure and test Azure AD single sign-on with Weekdone based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7c223-138">In this section, you configure and test Azure AD single sign-on with Weekdone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7c223-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Weekdone is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c223-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Weekdone is to a user in Azure AD.</span></span> <span data-ttu-id="7c223-140">In other words, a link relationship between an Azure AD user and the related user in Weekdone needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7c223-140">In other words, a link relationship between an Azure AD user and the related user in Weekdone needs to be established.</span></span>

<span data-ttu-id="7c223-141">To configure and test Azure AD single sign-on with Weekdone, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7c223-141">To configure and test Azure AD single sign-on with Weekdone, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7c223-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7c223-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7c223-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7c223-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7c223-144">**[Creating a Weekdone test user](#creating-a-weekdone-test-user)** - to have a counterpart of Britta Simon in Weekdone that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="7c223-144">**[Creating a Weekdone test user](#creating-a-weekdone-test-user)** - to have a counterpart of Britta Simon in Weekdone that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7c223-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7c223-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7c223-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7c223-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7c223-147">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7c223-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7c223-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Weekdone application.</span><span class="sxs-lookup"><span data-stu-id="7c223-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Weekdone application.</span></span>

<span data-ttu-id="7c223-149">**To configure Azure AD single sign-on with Weekdone, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7c223-149">**To configure Azure AD single sign-on with Weekdone, perform the following steps:**</span></span>

1. <span data-ttu-id="7c223-150">In the Azure portal, on the **Weekdone** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7c223-150">In the Azure portal, on the **Weekdone** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="7c223-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7c223-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/weekdone-tutorial/tutorial_weekdone_samlbase.png)

3. <span data-ttu-id="7c223-154">On the **Weekdone Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="7c223-154">On the **Weekdone Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/weekdone-tutorial/tutorial_weekdone_url1.png)

    <span data-ttu-id="7c223-156">a.</span><span class="sxs-lookup"><span data-stu-id="7c223-156">a.</span></span> <span data-ttu-id="7c223-157">In the **Identifier** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenant>/metadata`</span><span class="sxs-lookup"><span data-stu-id="7c223-157">In the **Identifier** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenant>/metadata`</span></span>

    > [!NOTE]
    > <span data-ttu-id="7c223-158">The metadata file from weekdone can be retrieved with using the same URL.</span><span class="sxs-lookup"><span data-stu-id="7c223-158">The metadata file from weekdone can be retrieved with using the same URL.</span></span>

    <span data-ttu-id="7c223-159">b.</span><span class="sxs-lookup"><span data-stu-id="7c223-159">b.</span></span> <span data-ttu-id="7c223-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="7c223-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

4. <span data-ttu-id="7c223-161">Check **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="7c223-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="7c223-162">If you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="7c223-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/weekdone-tutorial/tutorial_weekdone_url2.png)

    <span data-ttu-id="7c223-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="7c223-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="7c223-165">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="7c223-165">These values are not real.</span></span> <span data-ttu-id="7c223-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="7c223-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="7c223-167">Contact [Weekdone Client support team](mailto:hello@weekdone.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="7c223-167">Contact [Weekdone Client support team](mailto:hello@weekdone.com) to get these values.</span></span> 

5. <span data-ttu-id="7c223-168">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="7c223-168">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/weekdone-tutorial/tutorial_weekdone_certificate.png) 

6. <span data-ttu-id="7c223-170">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7c223-170">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/weekdone-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="7c223-172">On the **Weekdone Configuration** section, click **Configure Weekdone** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="7c223-172">On the **Weekdone Configuration** section, click **Configure Weekdone** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7c223-173">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="7c223-173">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/weekdone-tutorial/tutorial_weekdone_configure.png) 

8. <span data-ttu-id="7c223-175">To configure single sign-on on **Weekdone** side, you need to send the downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Weekdone support team](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="7c223-175">To configure single sign-on on **Weekdone** side, you need to send the downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Weekdone support team](mailto:hello@weekdone.com).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7c223-176">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7c223-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="7c223-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7c223-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="7c223-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7c223-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7c223-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7c223-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/weekdone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7c223-182">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="7c223-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/weekdone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7c223-184">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="7c223-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/weekdone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7c223-186">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7c223-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/weekdone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7c223-188">a.</span><span class="sxs-lookup"><span data-stu-id="7c223-188">a.</span></span> <span data-ttu-id="7c223-189">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7c223-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7c223-190">b.</span><span class="sxs-lookup"><span data-stu-id="7c223-190">b.</span></span> <span data-ttu-id="7c223-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7c223-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7c223-192">c.</span><span class="sxs-lookup"><span data-stu-id="7c223-192">c.</span></span> <span data-ttu-id="7c223-193">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="7c223-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7c223-194">d.</span><span class="sxs-lookup"><span data-stu-id="7c223-194">d.</span></span> <span data-ttu-id="7c223-195">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7c223-195">Click **Create**.</span></span>
 
### <a name="creating-a-weekdone-test-user"></a><span data-ttu-id="7c223-196">Creating a Weekdone test user</span><span class="sxs-lookup"><span data-stu-id="7c223-196">Creating a Weekdone test user</span></span>

<span data-ttu-id="7c223-197">The objective of this section is to create a user called Britta Simon in Weekdone.</span><span class="sxs-lookup"><span data-stu-id="7c223-197">The objective of this section is to create a user called Britta Simon in Weekdone.</span></span> <span data-ttu-id="7c223-198">Weekdone supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="7c223-198">Weekdone supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="7c223-199">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="7c223-199">There is no action item for you in this section.</span></span> <span data-ttu-id="7c223-200">A new user is created during an attempt to access Weekdone if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="7c223-200">A new user is created during an attempt to access Weekdone if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="7c223-201">If you need to create a user manually, you need to contact the [Weekdone Client support team](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="7c223-201">If you need to create a user manually, you need to contact the [Weekdone Client support team](mailto:hello@weekdone.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7c223-202">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7c223-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7c223-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Weekdone.</span><span class="sxs-lookup"><span data-stu-id="7c223-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Weekdone.</span></span>

![Assign User][200] 

<span data-ttu-id="7c223-205">**To assign Britta Simon to Weekdone, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7c223-205">**To assign Britta Simon to Weekdone, perform the following steps:**</span></span>

1. <span data-ttu-id="7c223-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7c223-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="7c223-208">In the applications list, select **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="7c223-208">In the applications list, select **Weekdone**.</span></span>

    ![Configure Single Sign-On](./media/weekdone-tutorial/tutorial_weekdone_app.png) 

3. <span data-ttu-id="7c223-210">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="7c223-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="7c223-212">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="7c223-212">Click **Add** button.</span></span> <span data-ttu-id="7c223-213">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7c223-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="7c223-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="7c223-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7c223-216">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="7c223-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7c223-217">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7c223-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7c223-218">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="7c223-218">Testing single sign-on</span></span>

<span data-ttu-id="7c223-219">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7c223-219">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="7c223-220">When you click the Weekdone tile in the Access Panel, you should get automatically signed-on to your Weekdone application.</span><span class="sxs-lookup"><span data-stu-id="7c223-220">When you click the Weekdone tile in the Access Panel, you should get automatically signed-on to your Weekdone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7c223-221">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7c223-221">Additional resources</span></span>

* [<span data-ttu-id="7c223-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c223-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="7c223-223">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7c223-223">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/weekdone-tutorial/tutorial_general_01.png
[2]: ./media/weekdone-tutorial/tutorial_general_02.png
[3]: ./media/weekdone-tutorial/tutorial_general_03.png
[4]: ./media/weekdone-tutorial/tutorial_general_04.png

[100]: ./media/weekdone-tutorial/tutorial_general_100.png

[200]: ./media/weekdone-tutorial/tutorial_general_200.png
[201]: ./media/weekdone-tutorial/tutorial_general_201.png
[202]: ./media/weekdone-tutorial/tutorial_general_202.png
[203]: ./media/weekdone-tutorial/tutorial_general_203.png
