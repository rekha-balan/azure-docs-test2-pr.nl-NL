---
title: 'Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and FirmPlay - Employee Advocacy for Recruiting.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 6e3d8a3951a42e448eff005b055b3cf5169179f1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856887"
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a><span data-ttu-id="5b23c-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="5b23c-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span></span>

<span data-ttu-id="5b23c-104">In this tutorial, you learn how to integrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5b23c-104">In this tutorial, you learn how to integrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b23c-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="5b23c-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5b23c-106">You can control in Azure AD who has access to FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="5b23c-106">You can control in Azure AD who has access to FirmPlay - Employee Advocacy for Recruiting</span></span>
- <span data-ttu-id="5b23c-107">You can enable your users to automatically get signed-on to FirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="5b23c-107">You can enable your users to automatically get signed-on to FirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5b23c-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="5b23c-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="5b23c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="5b23c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b23c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5b23c-110">Prerequisites</span></span>

<span data-ttu-id="5b23c-111">To configure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="5b23c-111">To configure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need the following items:</span></span>

- <span data-ttu-id="5b23c-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="5b23c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b23c-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="5b23c-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="5b23c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="5b23c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="5b23c-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="5b23c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b23c-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="5b23c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="5b23c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b23c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="5b23c-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="5b23c-118">Scenario description</span></span>
<span data-ttu-id="5b23c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="5b23c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b23c-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="5b23c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b23c-121">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span><span class="sxs-lookup"><span data-stu-id="5b23c-121">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
1. <span data-ttu-id="5b23c-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5b23c-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-the-gallery"></a><span data-ttu-id="5b23c-123">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span><span class="sxs-lookup"><span data-stu-id="5b23c-123">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
<span data-ttu-id="5b23c-124">To configure the integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need to add FirmPlay - Employee Advocacy for Recruiting from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="5b23c-124">To configure the integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need to add FirmPlay - Employee Advocacy for Recruiting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5b23c-125">**To add FirmPlay - Employee Advocacy for Recruiting from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5b23c-125">**To add FirmPlay - Employee Advocacy for Recruiting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5b23c-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="5b23c-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="5b23c-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="5b23c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5b23c-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="5b23c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="5b23c-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="5b23c-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="5b23c-133">In the search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span><span class="sxs-lookup"><span data-stu-id="5b23c-133">In the search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Creating an Azure AD test user](./media/firmplay-tutorial/tutorial_firmplay_001.png)

1. <span data-ttu-id="5b23c-135">In the results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="5b23c-135">In the results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5b23c-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5b23c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5b23c-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5b23c-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5b23c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FirmPlay - Employee Advocacy for Recruiting is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b23c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FirmPlay - Employee Advocacy for Recruiting is to a user in Azure AD.</span></span> <span data-ttu-id="5b23c-140">In other words, a link relationship between an Azure AD user and the related user in FirmPlay - Employee Advocacy for Recruiting needs to be established.</span><span class="sxs-lookup"><span data-stu-id="5b23c-140">In other words, a link relationship between an Azure AD user and the related user in FirmPlay - Employee Advocacy for Recruiting needs to be established.</span></span>

<span data-ttu-id="5b23c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="5b23c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FirmPlay - Employee Advocacy for Recruiting.</span></span>

<span data-ttu-id="5b23c-142">To configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="5b23c-142">To configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5b23c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="5b23c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="5b23c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b23c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="5b23c-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - to have a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="5b23c-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - to have a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked to the Azure AD representation of her.</span></span>
1. <span data-ttu-id="5b23c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5b23c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="5b23c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="5b23c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5b23c-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5b23c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5b23c-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span><span class="sxs-lookup"><span data-stu-id="5b23c-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span></span>

<span data-ttu-id="5b23c-150">**To configure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5b23c-150">**To configure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="5b23c-151">In the Azure Management portal, on the **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5b23c-151">In the Azure Management portal, on the **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="5b23c-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="5b23c-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](./media/firmplay-tutorial/tutorial_firmplay_01.png)

1. <span data-ttu-id="5b23c-155">On the **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.firmplay.com/`</span><span class="sxs-lookup"><span data-stu-id="5b23c-155">On the **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.firmplay.com/`</span></span>

    ![Configure Single Sign-On](./media/firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > <span data-ttu-id="5b23c-157">Please note that this is not the real value.</span><span class="sxs-lookup"><span data-stu-id="5b23c-157">Please note that this is not the real value.</span></span> <span data-ttu-id="5b23c-158">You have to update this value with the actual Sign On URL.</span><span class="sxs-lookup"><span data-stu-id="5b23c-158">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="5b23c-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="5b23c-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to get this value.</span></span> 

1. <span data-ttu-id="5b23c-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="5b23c-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configure Single Sign-On](./media/firmplay-tutorial/tutorial_firmplay_03.png)     

1. <span data-ttu-id="5b23c-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span><span class="sxs-lookup"><span data-stu-id="5b23c-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="5b23c-163">Then click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="5b23c-163">Then click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/firmplay-tutorial/tutorial_general_300.png)

1. <span data-ttu-id="5b23c-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="5b23c-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/firmplay-tutorial/tutorial_firmplay_04.png)

1. <span data-ttu-id="5b23c-167">On the pop-up **Rollover certificate** window, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5b23c-167">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configure Single Sign-On](./media/firmplay-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="5b23c-169">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="5b23c-169">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span> 

    ![Configure Single Sign-On](./media/firmplay-tutorial/tutorial_firmplay_05.png) 

1. <span data-ttu-id="5b23c-171">On the **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** to open **Configure sign-on** dialog.</span><span class="sxs-lookup"><span data-stu-id="5b23c-171">On the **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** to open **Configure sign-on** dialog.</span></span>

    ![Configure Single Sign-On](./media/firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Configure Single Sign-On](./media/firmplay-tutorial/tutorial_firmplay_07.png)

1. <span data-ttu-id="5b23c-174">To get SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="5b23c-174">To get SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with the following:</span></span> 

    <span data-ttu-id="5b23c-175">•  The downloaded **Certificate file**</span><span class="sxs-lookup"><span data-stu-id="5b23c-175">•  The downloaded **Certificate file**</span></span>

    <span data-ttu-id="5b23c-176">•  The **SAML Single Sign-On Service URL**</span><span class="sxs-lookup"><span data-stu-id="5b23c-176">•  The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="5b23c-177">•  The **SAML Entity ID**</span><span class="sxs-lookup"><span data-stu-id="5b23c-177">•  The **SAML Entity ID**</span></span>

    <span data-ttu-id="5b23c-178">•  The **Sign-Out URL**</span><span class="sxs-lookup"><span data-stu-id="5b23c-178">•  The **Sign-Out URL**</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5b23c-179">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5b23c-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="5b23c-180">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b23c-180">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="5b23c-182">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5b23c-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5b23c-183">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="5b23c-183">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/firmplay-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="5b23c-185">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="5b23c-185">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](./media/firmplay-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="5b23c-187">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="5b23c-187">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/firmplay-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="5b23c-189">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5b23c-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/firmplay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5b23c-191">a.</span><span class="sxs-lookup"><span data-stu-id="5b23c-191">a.</span></span> <span data-ttu-id="5b23c-192">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5b23c-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b23c-193">b.</span><span class="sxs-lookup"><span data-stu-id="5b23c-193">b.</span></span> <span data-ttu-id="5b23c-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5b23c-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5b23c-195">c.</span><span class="sxs-lookup"><span data-stu-id="5b23c-195">c.</span></span> <span data-ttu-id="5b23c-196">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="5b23c-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5b23c-197">d.</span><span class="sxs-lookup"><span data-stu-id="5b23c-197">d.</span></span> <span data-ttu-id="5b23c-198">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5b23c-198">Click **Create**.</span></span> 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a><span data-ttu-id="5b23c-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span><span class="sxs-lookup"><span data-stu-id="5b23c-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span></span>

<span data-ttu-id="5b23c-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="5b23c-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span></span> <span data-ttu-id="5b23c-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to add the users in the FirmPlay - Employee Advocacy for Recruiting platform.</span><span class="sxs-lookup"><span data-stu-id="5b23c-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to add the users in the FirmPlay - Employee Advocacy for Recruiting platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5b23c-202">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5b23c-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5b23c-203">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="5b23c-203">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FirmPlay - Employee Advocacy for Recruiting.</span></span>

![Assign User][200] 

<span data-ttu-id="5b23c-205">**To assign Britta Simon to FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5b23c-205">**To assign Britta Simon to FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="5b23c-206">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="5b23c-206">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="5b23c-208">In the applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span><span class="sxs-lookup"><span data-stu-id="5b23c-208">In the applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Configure Single Sign-On](./media/firmplay-tutorial/tutorial_firmplay_50.png) 

1. <span data-ttu-id="5b23c-210">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="5b23c-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="5b23c-212">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="5b23c-212">Click **Add** button.</span></span> <span data-ttu-id="5b23c-213">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="5b23c-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="5b23c-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="5b23c-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="5b23c-216">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="5b23c-216">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="5b23c-217">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="5b23c-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="5b23c-218">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="5b23c-218">Testing single sign-on</span></span>

<span data-ttu-id="5b23c-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="5b23c-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5b23c-220">When you click the FirmPlay - Employee Advocacy for Recruiting tile in the Access Panel, you should get automatically signed-on to your FirmPlay - Employee Advocacy for Recruiting application.</span><span class="sxs-lookup"><span data-stu-id="5b23c-220">When you click the FirmPlay - Employee Advocacy for Recruiting tile in the Access Panel, you should get automatically signed-on to your FirmPlay - Employee Advocacy for Recruiting application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="5b23c-221">Additional resources</span><span class="sxs-lookup"><span data-stu-id="5b23c-221">Additional resources</span></span>

* [<span data-ttu-id="5b23c-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b23c-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="5b23c-223">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5b23c-223">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/firmplay-tutorial/tutorial_general_01.png
[2]: ./media/firmplay-tutorial/tutorial_general_02.png
[3]: ./media/firmplay-tutorial/tutorial_general_03.png
[4]: ./media/firmplay-tutorial/tutorial_general_04.png

[100]: ./media/firmplay-tutorial/tutorial_general_100.png

[200]: ./media/firmplay-tutorial/tutorial_general_200.png
[201]: ./media/firmplay-tutorial/tutorial_general_201.png
[202]: ./media/firmplay-tutorial/tutorial_general_202.png
[203]: ./media/firmplay-tutorial/tutorial_general_203.png