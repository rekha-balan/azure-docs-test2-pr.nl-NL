---
title: 'Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and IBM Kenexa Survey Enterprise.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: 8db48feb34fa488abd0ab2dcb1ab15478bdde3e1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562921"
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a><span data-ttu-id="3bc5d-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="3bc5d-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span></span>
<span data-ttu-id="3bc5d-104">In this tutorial, you learn how to integrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3bc5d-104">In this tutorial, you learn how to integrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3bc5d-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3bc5d-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="3bc5d-106">You can control in Azure AD who has access to IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="3bc5d-106">You can control in Azure AD who has access to IBM Kenexa Survey Enterprise</span></span>
* <span data-ttu-id="3bc5d-107">You can enable your users to automatically get signed-on to IBM Kenexa Survey Enterprise single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="3bc5d-107">You can enable your users to automatically get signed-on to IBM Kenexa Survey Enterprise single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="3bc5d-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="3bc5d-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="3bc5d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3bc5d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3bc5d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3bc5d-110">Prerequisites</span></span>
<span data-ttu-id="3bc5d-111">To configure Azure AD integration with IBM Kenexa Survey Enterprise, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="3bc5d-111">To configure Azure AD integration with IBM Kenexa Survey Enterprise, you need the following items:</span></span>

* <span data-ttu-id="3bc5d-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="3bc5d-112">An Azure AD subscription</span></span>
* <span data-ttu-id="3bc5d-113">A IBM Kenexa Survey Enterprise SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="3bc5d-113">A IBM Kenexa Survey Enterprise SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="3bc5d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="3bc5d-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="3bc5d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="3bc5d-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="3bc5d-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3bc5d-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3bc5d-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="3bc5d-118">Scenario description</span></span>
<span data-ttu-id="3bc5d-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="3bc5d-120">The scenariofd outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="3bc5d-120">The scenariofd outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3bc5d-121">Adding IBM Kenexa Survey Enterprise from the gallery</span><span class="sxs-lookup"><span data-stu-id="3bc5d-121">Adding IBM Kenexa Survey Enterprise from the gallery</span></span>
2. <span data-ttu-id="3bc5d-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="3bc5d-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-ibm-kenexa-survey-enterprise-from-the-gallery"></a><span data-ttu-id="3bc5d-123">Adding IBM Kenexa Survey Enterprise from the gallery</span><span class="sxs-lookup"><span data-stu-id="3bc5d-123">Adding IBM Kenexa Survey Enterprise from the gallery</span></span>
<span data-ttu-id="3bc5d-124">To configure the integration of IBM Kenexa Survey Enterprise into Azure AD, you need to add IBM Kenexa Survey Enterprise from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-124">To configure the integration of IBM Kenexa Survey Enterprise into Azure AD, you need to add IBM Kenexa Survey Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3bc5d-125">**To add IBM Kenexa Survey Enterprise from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3bc5d-125">**To add IBM Kenexa Survey Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3bc5d-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="3bc5d-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="3bc5d-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="3bc5d-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="3bc5d-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="3bc5d-135">In the search box, type **IBM Kenexa Survey Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-135">In the search box, type **IBM Kenexa Survey Enterprise**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_01.png)
7. <span data-ttu-id="3bc5d-137">In the results pane, select **IBM Kenexa Survey Enterprise**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-137">In the results pane, select **IBM Kenexa Survey Enterprise**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_02.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3bc5d-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3bc5d-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="3bc5d-140">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3bc5d-140">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3bc5d-141">For SSO to work, Azure AD needs to know what the counterpart user in IBM Kenexa Survey Enterprise is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-141">For SSO to work, Azure AD needs to know what the counterpart user in IBM Kenexa Survey Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="3bc5d-142">In other words, a link relationship between an Azure AD user and the related user in IBM Kenexa Survey Enterprise needs to be established.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-142">In other words, a link relationship between an Azure AD user and the related user in IBM Kenexa Survey Enterprise needs to be established.</span></span>

<span data-ttu-id="3bc5d-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in IBM Kenexa Survey Enterprise.</span></span>

<span data-ttu-id="3bc5d-144">To configure and test Azure AD SSO with IBM Kenexa Survey Enterprise, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="3bc5d-144">To configure and test Azure AD SSO with IBM Kenexa Survey Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3bc5d-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3bc5d-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3bc5d-147">**[Creating an IBM Kenexa Survey Enterprise test user](#creating-an-kenexasurvey-test-user)** - to have a counterpart of Britta Simon in IBM Kenexa Survey Enterprise that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-147">**[Creating an IBM Kenexa Survey Enterprise test user](#creating-an-kenexasurvey-test-user)** - to have a counterpart of Britta Simon in IBM Kenexa Survey Enterprise that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="3bc5d-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3bc5d-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3bc5d-150">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3bc5d-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="3bc5d-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your IBM Kenexa Survey Enterprise application.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your IBM Kenexa Survey Enterprise application.</span></span>

<span data-ttu-id="3bc5d-152">**To configure Azure AD single sign-on with IBM Kenexa Survey Enterprise, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3bc5d-152">**To configure Azure AD single sign-on with IBM Kenexa Survey Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="3bc5d-153">In the classic portal, on the **IBM Kenexa Survey Enterprise** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-153">In the classic portal, on the **IBM Kenexa Survey Enterprise** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="3bc5d-155">On the **How would you like users to sign on to IBM Kenexa Survey Enterprise** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-155">On the **How would you like users to sign on to IBM Kenexa Survey Enterprise** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_03.png)
3. <span data-ttu-id="3bc5d-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3bc5d-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_04.png)
  1. <span data-ttu-id="3bc5d-159">In the **Identifier** textbox, type a URL using the following pattern: `https://surveys.kenexa.com/<company code>`</span><span class="sxs-lookup"><span data-stu-id="3bc5d-159">In the **Identifier** textbox, type a URL using the following pattern: `https://surveys.kenexa.com/<company code>`</span></span> 
  2. <span data-ttu-id="3bc5d-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://surveys.kenexa.com/<company code>/tools/sso.asp`</span><span class="sxs-lookup"><span data-stu-id="3bc5d-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://surveys.kenexa.com/<company code>/tools/sso.asp`</span></span>
  3. <span data-ttu-id="3bc5d-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-161">Click **Next**.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="3bc5d-162">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-162">Please note that these are not the real values.</span></span> <span data-ttu-id="3bc5d-163">You have to update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-163">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="3bc5d-164">Contact IBM Kenexa Survey Enterprise support team to get these values.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-164">Contact IBM Kenexa Survey Enterprise support team to get these values.</span></span> 
   > 
4. <span data-ttu-id="3bc5d-165">On the **Configure single sign-on at IBM Kenexa Survey Enterprise** page, click **Download certificate** and then save the file on your computer:</span><span class="sxs-lookup"><span data-stu-id="3bc5d-165">On the **Configure single sign-on at IBM Kenexa Survey Enterprise** page, click **Download certificate** and then save the file on your computer:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_05.png) 
5. <span data-ttu-id="3bc5d-167">To get SSO configured for your application, contact IBM Kenexa support team and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="3bc5d-167">To get SSO configured for your application, contact IBM Kenexa support team and provide them with the following:</span></span>
 * <span data-ttu-id="3bc5d-168">The downloaded certificate file</span><span class="sxs-lookup"><span data-stu-id="3bc5d-168">The downloaded certificate file</span></span>
 * <span data-ttu-id="3bc5d-169">The **Issuer URL**</span><span class="sxs-lookup"><span data-stu-id="3bc5d-169">The **Issuer URL**</span></span>  
 * <span data-ttu-id="3bc5d-170">The **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="3bc5d-170">The **SAML SSO URL**</span></span>
 * <span data-ttu-id="3bc5d-171">The **Single Sign-Out Service URL**</span><span class="sxs-lookup"><span data-stu-id="3bc5d-171">The **Single Sign-Out Service URL**</span></span>
   
  >[!NOTE]
  ><span data-ttu-id="3bc5d-172">Please note that NameID claim value in the Response has to match with SSO ID configured in Kenexa system.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-172">Please note that NameID claim value in the Response has to match with SSO ID configured in Kenexa system.</span></span> <span data-ttu-id="3bc5d-173">So please work with Kenexa support team to map the appropriate user identifier in your organization as SSO ID.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-173">So please work with Kenexa support team to map the appropriate user identifier in your organization as SSO ID.</span></span> <span data-ttu-id="3bc5d-174">By default Azure AD will set the NameIdentifier as UPN value.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-174">By default Azure AD will set the NameIdentifier as UPN value.</span></span> <span data-ttu-id="3bc5d-175">You can change this from Attribute tab as shown in the screenshot below.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-175">You can change this from Attribute tab as shown in the screenshot below.</span></span> <span data-ttu-id="3bc5d-176">The integration will only work after completing the correct mapping.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-176">The integration will only work after completing the correct mapping.</span></span> 
  > 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_51.png)
6. <span data-ttu-id="3bc5d-178">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-178">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="3bc5d-180">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-180">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]
8. <span data-ttu-id="3bc5d-182">In the Azure classic portal, on the **IBM Kenexa Survey Enterprise** application integration page, in the menu on the top, click **Attributes**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-182">In the Azure classic portal, on the **IBM Kenexa Survey Enterprise** application integration page, in the menu on the top, click **Attributes**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_06.png)
9. <span data-ttu-id="3bc5d-184">On the **SAML token attributes** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3bc5d-184">On the **SAML token attributes** dialog, perform the following steps:</span></span>
 1. <span data-ttu-id="3bc5d-185">Select the attribute of **NameIdentifier** and click **Edit** icon.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-185">Select the attribute of **NameIdentifier** and click **Edit** icon.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_07.png)  
 2. <span data-ttu-id="3bc5d-187">From the **Attribute Value** list, type the attribute value of SSO ID which is configured in Kenexa system.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-187">From the **Attribute Value** list, type the attribute value of SSO ID which is configured in Kenexa system.</span></span>  
 3. <span data-ttu-id="3bc5d-188">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-188">Click **Complete**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3bc5d-189">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3bc5d-189">Create an Azure AD test user</span></span>
<span data-ttu-id="3bc5d-190">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-190">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="3bc5d-192">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3bc5d-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3bc5d-193">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-193">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="3bc5d-195">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-195">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="3bc5d-196">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-196">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="3bc5d-198">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-198">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="3bc5d-200">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3bc5d-200">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_05.png) 
 1. <span data-ttu-id="3bc5d-202">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-202">As Type Of User, select New user in your organization.</span></span> 
 2. <span data-ttu-id="3bc5d-203">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-203">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="3bc5d-204">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-204">Click **Next**.</span></span>
6. <span data-ttu-id="3bc5d-205">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3bc5d-205">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="3bc5d-207">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-207">In the **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="3bc5d-208">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-208">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="3bc5d-209">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-209">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="3bc5d-210">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-210">In the **Role** list, select **User**.</span></span> 
 5. <span data-ttu-id="3bc5d-211">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-211">Click **Next**.</span></span>
7. <span data-ttu-id="3bc5d-212">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-212">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="3bc5d-214">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3bc5d-214">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="3bc5d-216">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-216">Write down the value of the **New Password**.</span></span>  
 2. <span data-ttu-id="3bc5d-217">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-217">Click **Complete**.</span></span>   

### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a><span data-ttu-id="3bc5d-218">Create an IBM Kenexa Survey Enterprise test user</span><span class="sxs-lookup"><span data-stu-id="3bc5d-218">Create an IBM Kenexa Survey Enterprise test user</span></span>
<span data-ttu-id="3bc5d-219">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-219">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span></span> 

<span data-ttu-id="3bc5d-220">You can work with IBM Kenexa support team to map the SSO ID for all the users.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-220">You can work with IBM Kenexa support team to map the SSO ID for all the users.</span></span> <span data-ttu-id="3bc5d-221">Also this SSO ID value should be mapped to the NameIdentifier value from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-221">Also this SSO ID value should be mapped to the NameIdentifier value from Azure AD.</span></span> <span data-ttu-id="3bc5d-222">You can change this default settings in the Attribute tab.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-222">You can change this default settings in the Attribute tab.</span></span>

>[!NOTE]
><span data-ttu-id="3bc5d-223">If you need to create a user manually, you need to contact the IBM Kenexa Survey Enterprise support team.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-223">If you need to create a user manually, you need to contact the IBM Kenexa Survey Enterprise support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3bc5d-224">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3bc5d-224">Assign the Azure AD test user</span></span>
<span data-ttu-id="3bc5d-225">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-225">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to IBM Kenexa Survey Enterprise.</span></span>

![Assign User][200] 

<span data-ttu-id="3bc5d-227">**To assign Britta Simon to IBM Kenexa Survey Enterprise, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3bc5d-227">**To assign Britta Simon to IBM Kenexa Survey Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="3bc5d-228">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-228">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="3bc5d-230">In the applications list, select **IBM Kenexa Survey Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-230">In the applications list, select **IBM Kenexa Survey Enterprise**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_50.png) 
3. <span data-ttu-id="3bc5d-232">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-232">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="3bc5d-234">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-234">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="3bc5d-235">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-235">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="3bc5d-237">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="3bc5d-237">Test single sign-on</span></span>
<span data-ttu-id="3bc5d-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3bc5d-239">When you click the IBM Kenexa Survey Enterprise tile in the Access Panel, you should get automatically signed-on to your IBM Kenexa Survey Enterprise application.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-239">When you click the IBM Kenexa Survey Enterprise tile in the Access Panel, you should get automatically signed-on to your IBM Kenexa Survey Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3bc5d-240">Additional resources</span><span class="sxs-lookup"><span data-stu-id="3bc5d-240">Additional resources</span></span>
* [<span data-ttu-id="3bc5d-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3bc5d-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3bc5d-242">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3bc5d-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_205.png




























