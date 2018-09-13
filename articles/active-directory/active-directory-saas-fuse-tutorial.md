---
title: 'Tutorial: Azure Active Directory integration with Fuse | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Fuse.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5ef34f58-863a-4b37-875c-e8efa3e18bb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: 69fb88787cf4327da7d85a14df143bfa62ea4ee7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551210"
---
# <a name="tutorial-azure-active-directory-integration-with-fuse"></a><span data-ttu-id="be7fa-103">Tutorial: Azure Active Directory integration with Fuse</span><span class="sxs-lookup"><span data-stu-id="be7fa-103">Tutorial: Azure Active Directory integration with Fuse</span></span>

<span data-ttu-id="be7fa-104">In this tutorial, you learn how to integrate Fuse with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="be7fa-104">In this tutorial, you learn how to integrate Fuse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="be7fa-105">Integrating Fuse with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="be7fa-105">Integrating Fuse with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="be7fa-106">You can control in Azure AD who has access to Fuse</span><span class="sxs-lookup"><span data-stu-id="be7fa-106">You can control in Azure AD who has access to Fuse</span></span>
- <span data-ttu-id="be7fa-107">You can enable your users to automatically get signed-on to Fuse (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="be7fa-107">You can enable your users to automatically get signed-on to Fuse (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="be7fa-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="be7fa-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="be7fa-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="be7fa-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be7fa-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="be7fa-110">Prerequisites</span></span>

<span data-ttu-id="be7fa-111">To configure Azure AD integration with Fuse, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="be7fa-111">To configure Azure AD integration with Fuse, you need the following items:</span></span>

- <span data-ttu-id="be7fa-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="be7fa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="be7fa-113">A Fuse single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="be7fa-113">A Fuse single-sign on (SSO) enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="be7fa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="be7fa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>
>

<span data-ttu-id="be7fa-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="be7fa-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="be7fa-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="be7fa-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="be7fa-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="be7fa-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="be7fa-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="be7fa-118">Scenario description</span></span>
<span data-ttu-id="be7fa-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="be7fa-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="be7fa-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="be7fa-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="be7fa-121">Adding Fuse from the gallery</span><span class="sxs-lookup"><span data-stu-id="be7fa-121">Adding Fuse from the gallery</span></span>
2. <span data-ttu-id="be7fa-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="be7fa-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-fuse-from-the-gallery"></a><span data-ttu-id="be7fa-123">Add Fuse from the gallery</span><span class="sxs-lookup"><span data-stu-id="be7fa-123">Add Fuse from the gallery</span></span>
<span data-ttu-id="be7fa-124">To configure the integration of Fuse into Azure AD, you need to add Fuse from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="be7fa-124">To configure the integration of Fuse into Azure AD, you need to add Fuse from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="be7fa-125">**To add Fuse from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="be7fa-125">**To add Fuse from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="be7fa-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="be7fa-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="be7fa-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="be7fa-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="be7fa-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="be7fa-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="be7fa-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="be7fa-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="be7fa-133">In the search box, type **Fuse**.</span><span class="sxs-lookup"><span data-stu-id="be7fa-133">In the search box, type **Fuse**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_fuse_001.png)

5. <span data-ttu-id="be7fa-135">In the results panel, select **Fuse**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="be7fa-135">In the results panel, select **Fuse**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_fuse_0001.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="be7fa-137">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="be7fa-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="be7fa-138">In this section, you configure and test Azure AD SSO with Fuse based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="be7fa-138">In this section, you configure and test Azure AD SSO with Fuse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="be7fa-139">For SSO to work, Azure AD needs to know what the counterpart user in Fuse is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be7fa-139">For SSO to work, Azure AD needs to know what the counterpart user in Fuse is to a user in Azure AD.</span></span> <span data-ttu-id="be7fa-140">In other words, a link relationship between an Azure AD user and the related user in Fuse needs to be established.</span><span class="sxs-lookup"><span data-stu-id="be7fa-140">In other words, a link relationship between an Azure AD user and the related user in Fuse needs to be established.</span></span>

<span data-ttu-id="be7fa-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Fuse.</span><span class="sxs-lookup"><span data-stu-id="be7fa-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Fuse.</span></span>

<span data-ttu-id="be7fa-142">To configure and test Azure AD SSO with Fuse, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="be7fa-142">To configure and test Azure AD SSO with Fuse, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="be7fa-143">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="be7fa-143">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="be7fa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="be7fa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="be7fa-145">**[Creating a Fuse test user](#creating-a-fuse-test-user)** - to have a counterpart of Britta Simon in Fuse that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="be7fa-145">**[Creating a Fuse test user](#creating-a-fuse-test-user)** - to have a counterpart of Britta Simon in Fuse that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="be7fa-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="be7fa-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="be7fa-147">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="be7fa-147">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="be7fa-148">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="be7fa-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="be7fa-149">In this section, you enable Azure AD SSO in the Azure Management portal and configure SSO in your Fuse application.</span><span class="sxs-lookup"><span data-stu-id="be7fa-149">In this section, you enable Azure AD SSO in the Azure Management portal and configure SSO in your Fuse application.</span></span>

<span data-ttu-id="be7fa-150">**To configure Azure AD SSO with Fuse, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="be7fa-150">**To configure Azure AD SSO with Fuse, perform the following steps:**</span></span>

1. <span data-ttu-id="be7fa-151">In the Azure Management portal, on the **Fuse** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="be7fa-151">In the Azure Management portal, on the **Fuse** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="be7fa-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="be7fa-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_fuse_01.png)

3. <span data-ttu-id="be7fa-155">On the **Fuse Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="be7fa-155">On the **Fuse Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_fuse_02.png)
  1. <span data-ttu-id="be7fa-157">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<tenant name>.fusion-universal.com/`</span><span class="sxs-lookup"><span data-stu-id="be7fa-157">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<tenant name>.fusion-universal.com/`</span></span>
  2. <span data-ttu-id="be7fa-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant name>.fusion-universal.com`</span><span class="sxs-lookup"><span data-stu-id="be7fa-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant name>.fusion-universal.com`</span></span>

      >[!NOTE] 
      ><span data-ttu-id="be7fa-159">These are not the real values.</span><span class="sxs-lookup"><span data-stu-id="be7fa-159">These are not the real values.</span></span> <span data-ttu-id="be7fa-160">You have to update these values with the actual Sign On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="be7fa-160">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="be7fa-161">Contact [Fuse support team](mailto:support@fusion-universal.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="be7fa-161">Contact [Fuse support team](mailto:support@fusion-universal.com) to get these values.</span></span> 
      >
      >

4. <span data-ttu-id="be7fa-162">On the **SAML Signing Certificate** section, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="be7fa-162">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_fuse_03.png)  

5. <span data-ttu-id="be7fa-164">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span><span class="sxs-lookup"><span data-stu-id="be7fa-164">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="be7fa-165">Then click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="be7fa-165">Then click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="be7fa-167">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="be7fa-167">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_fuse_04.png)

7. <span data-ttu-id="be7fa-169">On the pop-up **Rollover certificate** window, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="be7fa-169">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="be7fa-171">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="be7fa-171">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_fuse_05.png) 

9. <span data-ttu-id="be7fa-173">On the **Fuse Configuration** section, click **Configure Fuse** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="be7fa-173">On the **Fuse Configuration** section, click **Configure Fuse** to open **Configure sign-on** window.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_fuse_06.png) 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_fuse_07.png)

10. <span data-ttu-id="be7fa-176">To get SSO configured for your application, contact [Fuse support team](mailto:support@fusion-universal.com) and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="be7fa-176">To get SSO configured for your application, contact [Fuse support team](mailto:support@fusion-universal.com) and provide them with the following:</span></span> 

    <span data-ttu-id="be7fa-177">•  The downloaded **Certificate file** •  The **SAML Single Sign-On Service URL** •  The **SAML Entity ID** •  The **Sign-Out URL**</span><span class="sxs-lookup"><span data-stu-id="be7fa-177">•  The downloaded **Certificate file** •  The **SAML Single Sign-On Service URL** •  The **SAML Entity ID** •  The **Sign-Out URL**</span></span>
  
### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="be7fa-178">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="be7fa-178">Create an Azure AD test user</span></span>
<span data-ttu-id="be7fa-179">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="be7fa-179">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="be7fa-181">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="be7fa-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="be7fa-182">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="be7fa-182">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="be7fa-184">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="be7fa-184">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="be7fa-186">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="be7fa-186">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="be7fa-188">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="be7fa-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="be7fa-190">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="be7fa-190">In the **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="be7fa-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="be7fa-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="be7fa-192">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="be7fa-192">Select **Show Password** and write down the value of the **Password**.</span></span>
  4. <span data-ttu-id="be7fa-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="be7fa-193">Click **Create**.</span></span> 

### <a name="create-a-fuse-test-user"></a><span data-ttu-id="be7fa-194">Create a Fuse test user</span><span class="sxs-lookup"><span data-stu-id="be7fa-194">Create a Fuse test user</span></span>

<span data-ttu-id="be7fa-195">In this section, you create a user called Britta Simon in Fuse.</span><span class="sxs-lookup"><span data-stu-id="be7fa-195">In this section, you create a user called Britta Simon in Fuse.</span></span> <span data-ttu-id="be7fa-196">Please work with [Fuse support team](mailto:support@fusion-universal.com) to add the users in the Fuse platform.</span><span class="sxs-lookup"><span data-stu-id="be7fa-196">Please work with [Fuse support team](mailto:support@fusion-universal.com) to add the users in the Fuse platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="be7fa-197">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="be7fa-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="be7fa-198">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Fuse.</span><span class="sxs-lookup"><span data-stu-id="be7fa-198">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Fuse.</span></span>

![Assign User][200] 

<span data-ttu-id="be7fa-200">**To assign Britta Simon to Fuse, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="be7fa-200">**To assign Britta Simon to Fuse, perform the following steps:**</span></span>

1. <span data-ttu-id="be7fa-201">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="be7fa-201">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="be7fa-203">In the applications list, select **Fuse**.</span><span class="sxs-lookup"><span data-stu-id="be7fa-203">In the applications list, select **Fuse**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_fuse_50.png) 

3. <span data-ttu-id="be7fa-205">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="be7fa-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="be7fa-207">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="be7fa-207">Click **Add** button.</span></span> <span data-ttu-id="be7fa-208">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="be7fa-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="be7fa-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="be7fa-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="be7fa-211">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="be7fa-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="be7fa-212">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="be7fa-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="be7fa-213">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="be7fa-213">Test single sign-on</span></span>

<span data-ttu-id="be7fa-214">In this section, you test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="be7fa-214">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="be7fa-215">When you click the Fuse tile in the Access Panel, you should get automatically signed-on to your Fuse application.</span><span class="sxs-lookup"><span data-stu-id="be7fa-215">When you click the Fuse tile in the Access Panel, you should get automatically signed-on to your Fuse application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="be7fa-216">Additional resources</span><span class="sxs-lookup"><span data-stu-id="be7fa-216">Additional resources</span></span>

* [<span data-ttu-id="be7fa-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="be7fa-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="be7fa-218">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="be7fa-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuse-tutorial/tutorial_general_203.png

























