---
title: 'Tutorial: Azure Active Directory integration with MaxxPoint | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and MaxxPoint.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ba026e-96fc-4ae8-b135-0169da810e99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 19b43e3c5d17e80cc7c74cc768d3dcd7421fb7e9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662650"
---
# <a name="tutorial-azure-active-directory-integration-with-maxxpoint"></a><span data-ttu-id="add50-103">Tutorial: Azure Active Directory integration with MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="add50-103">Tutorial: Azure Active Directory integration with MaxxPoint</span></span>

<span data-ttu-id="add50-104">In this tutorial, you learn how to integrate MaxxPoint with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="add50-104">In this tutorial, you learn how to integrate MaxxPoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="add50-105">Integrating MaxxPoint with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="add50-105">Integrating MaxxPoint with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="add50-106">You can control in Azure AD who has access to MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="add50-106">You can control in Azure AD who has access to MaxxPoint</span></span>
- <span data-ttu-id="add50-107">You can enable your users to automatically get signed-on to MaxxPoint (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="add50-107">You can enable your users to automatically get signed-on to MaxxPoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="add50-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="add50-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="add50-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="add50-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="add50-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="add50-110">Prerequisites</span></span>

<span data-ttu-id="add50-111">To configure Azure AD integration with MaxxPoint, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="add50-111">To configure Azure AD integration with MaxxPoint, you need the following items:</span></span>

- <span data-ttu-id="add50-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="add50-112">An Azure AD subscription</span></span>
- <span data-ttu-id="add50-113">A MaxxPoint single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="add50-113">A MaxxPoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="add50-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="add50-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="add50-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="add50-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="add50-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="add50-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="add50-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="add50-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="add50-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="add50-118">Scenario description</span></span>
<span data-ttu-id="add50-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="add50-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="add50-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="add50-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="add50-121">Adding MaxxPoint from the gallery</span><span class="sxs-lookup"><span data-stu-id="add50-121">Adding MaxxPoint from the gallery</span></span>
2. <span data-ttu-id="add50-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="add50-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-maxxpoint-from-the-gallery"></a><span data-ttu-id="add50-123">Adding MaxxPoint from the gallery</span><span class="sxs-lookup"><span data-stu-id="add50-123">Adding MaxxPoint from the gallery</span></span>
<span data-ttu-id="add50-124">To configure the integration of MaxxPoint into Azure AD, you need to add MaxxPoint from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="add50-124">To configure the integration of MaxxPoint into Azure AD, you need to add MaxxPoint from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="add50-125">**To add MaxxPoint from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="add50-125">**To add MaxxPoint from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="add50-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="add50-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="add50-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="add50-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="add50-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="add50-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="add50-131">Click **New application** button on the top of dialog to add new application.</span><span class="sxs-lookup"><span data-stu-id="add50-131">Click **New application** button on the top of dialog to add new application.</span></span>

    ![Applications][3]

4. <span data-ttu-id="add50-133">In the search box, type **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="add50-133">In the search box, type **MaxxPoint**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_001.png)

5. <span data-ttu-id="add50-135">In the results panel, select **MaxxPoint**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="add50-135">In the results panel, select **MaxxPoint**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="add50-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="add50-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="add50-138">In this section, you configure and test Azure AD single sign-on with MaxxPoint based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="add50-138">In this section, you configure and test Azure AD single sign-on with MaxxPoint based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="add50-139">For single sign-on to work, Azure AD needs to know what the counterpart user in MaxxPoint is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="add50-139">For single sign-on to work, Azure AD needs to know what the counterpart user in MaxxPoint is to a user in Azure AD.</span></span> <span data-ttu-id="add50-140">In other words, a link relationship between an Azure AD user and the related user in MaxxPoint needs to be established.</span><span class="sxs-lookup"><span data-stu-id="add50-140">In other words, a link relationship between an Azure AD user and the related user in MaxxPoint needs to be established.</span></span>

<span data-ttu-id="add50-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="add50-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in MaxxPoint.</span></span>

<span data-ttu-id="add50-142">To configure and test Azure AD single sign-on with MaxxPoint, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="add50-142">To configure and test Azure AD single sign-on with MaxxPoint, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="add50-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="add50-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="add50-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="add50-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="add50-145">**[Creating a MaxxPoint test user](#creating-a-maxxpoint-test-user)** - to have a counterpart of Britta Simon in MaxxPoint that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="add50-145">**[Creating a MaxxPoint test user](#creating-a-maxxpoint-test-user)** - to have a counterpart of Britta Simon in MaxxPoint that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="add50-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="add50-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="add50-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="add50-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="add50-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="add50-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="add50-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MaxxPoint application.</span><span class="sxs-lookup"><span data-stu-id="add50-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MaxxPoint application.</span></span>

<span data-ttu-id="add50-150">**To configure Azure AD single sign-on with MaxxPoint, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="add50-150">**To configure Azure AD single sign-on with MaxxPoint, perform the following steps:**</span></span>

1. <span data-ttu-id="add50-151">In the Azure portal, on the **MaxxPoint** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="add50-151">In the Azure portal, on the **MaxxPoint** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="add50-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="add50-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/tutorial_general_300.png)

3. <span data-ttu-id="add50-155">On the **MaxxPoint Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, no need to perform any steps.</span><span class="sxs-lookup"><span data-stu-id="add50-155">On the **MaxxPoint Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, no need to perform any steps.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_02.png)
    
4. <span data-ttu-id="add50-157">On the **MaxxPoint Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="add50-157">On the **MaxxPoint Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_03.png)

    <span data-ttu-id="add50-159">a.</span><span class="sxs-lookup"><span data-stu-id="add50-159">a.</span></span> <span data-ttu-id="add50-160">Click **Show advanced URL settings** option</span><span class="sxs-lookup"><span data-stu-id="add50-160">Click **Show advanced URL settings** option</span></span>

    <span data-ttu-id="add50-161">b.</span><span class="sxs-lookup"><span data-stu-id="add50-161">b.</span></span> <span data-ttu-id="add50-162">In the **Sign On URL** textbox, type a URL using the following pattern: `https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span><span class="sxs-lookup"><span data-stu-id="add50-162">In the **Sign On URL** textbox, type a URL using the following pattern: `https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="add50-163">Please note that this is not the real value.</span><span class="sxs-lookup"><span data-stu-id="add50-163">Please note that this is not the real value.</span></span> <span data-ttu-id="add50-164">You have to update this value with the actual Sign On URL.</span><span class="sxs-lookup"><span data-stu-id="add50-164">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="add50-165">Call MaxxPoint team on **888-728-0950** to get this value.</span><span class="sxs-lookup"><span data-stu-id="add50-165">Call MaxxPoint team on **888-728-0950** to get this value.</span></span>

5. <span data-ttu-id="add50-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="add50-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_06.png) 

6. <span data-ttu-id="add50-168">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="add50-168">Click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="add50-170">To get SSO configured for your application, call MaxxPoint support team on **888-728-0950** and they'll assist you further on how to provide them the downloaded **Metadata XML** file.</span><span class="sxs-lookup"><span data-stu-id="add50-170">To get SSO configured for your application, call MaxxPoint support team on **888-728-0950** and they'll assist you further on how to provide them the downloaded **Metadata XML** file.</span></span> 

> [!TIP]
> <span data-ttu-id="add50-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="add50-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="add50-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="add50-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="add50-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="add50-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="add50-174">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="add50-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="add50-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="add50-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="add50-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="add50-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="add50-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="add50-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="add50-180">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="add50-180">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="add50-182">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="add50-182">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="add50-184">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="add50-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="add50-186">a.</span><span class="sxs-lookup"><span data-stu-id="add50-186">a.</span></span> <span data-ttu-id="add50-187">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="add50-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="add50-188">b.</span><span class="sxs-lookup"><span data-stu-id="add50-188">b.</span></span> <span data-ttu-id="add50-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="add50-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="add50-190">c.</span><span class="sxs-lookup"><span data-stu-id="add50-190">c.</span></span> <span data-ttu-id="add50-191">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="add50-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="add50-192">d.</span><span class="sxs-lookup"><span data-stu-id="add50-192">d.</span></span> <span data-ttu-id="add50-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="add50-193">Click **Create**.</span></span> 

### <a name="creating-a-maxxpoint-test-user"></a><span data-ttu-id="add50-194">Creating a MaxxPoint test user</span><span class="sxs-lookup"><span data-stu-id="add50-194">Creating a MaxxPoint test user</span></span>

<span data-ttu-id="add50-195">In this section, you create a user called Britta Simon in MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="add50-195">In this section, you create a user called Britta Simon in MaxxPoint.</span></span> <span data-ttu-id="add50-196">Please call MaxxPoint support team on **888-728-0950** to add the users in the MaxxPoint application.</span><span class="sxs-lookup"><span data-stu-id="add50-196">Please call MaxxPoint support team on **888-728-0950** to add the users in the MaxxPoint application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="add50-197">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="add50-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="add50-198">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="add50-198">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to MaxxPoint.</span></span>

![Assign User][200] 

<span data-ttu-id="add50-200">**To assign Britta Simon to MaxxPoint, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="add50-200">**To assign Britta Simon to MaxxPoint, perform the following steps:**</span></span>

1. <span data-ttu-id="add50-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="add50-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="add50-203">In the applications list, select **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="add50-203">In the applications list, select **MaxxPoint**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_50.png) 

3. <span data-ttu-id="add50-205">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="add50-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="add50-207">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="add50-207">Click **Add** button.</span></span> <span data-ttu-id="add50-208">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="add50-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="add50-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="add50-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="add50-211">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="add50-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="add50-212">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="add50-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="add50-213">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="add50-213">Testing single sign-on</span></span>

<span data-ttu-id="add50-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="add50-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="add50-215">When you click the MaxxPoint tile in the Access Panel, you should get automatically signed-on to your MaxxPoint application.</span><span class="sxs-lookup"><span data-stu-id="add50-215">When you click the MaxxPoint tile in the Access Panel, you should get automatically signed-on to your MaxxPoint application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="add50-216">Additional resources</span><span class="sxs-lookup"><span data-stu-id="add50-216">Additional resources</span></span>

* [<span data-ttu-id="add50-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="add50-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="add50-218">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="add50-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-maxxpoint-tutorial/tutorial_general_203.png




















