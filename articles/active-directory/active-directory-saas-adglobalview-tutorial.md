---
title: 'Tutorial: Azure Active Directory integration with ADP GlobalView | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ADP GlobalView.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: ffb6464f-714d-41a9-869a-2b7e5ae9f125
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2017
ms.author: jeedes
ms.openlocfilehash: 3def36fb5bfc4e35ac96022dddff57506820efbc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549406"
---
# <a name="tutorial-azure-active-directory-integration-with-adp-globalview"></a><span data-ttu-id="c9b2e-103">Tutorial: Azure Active Directory integration with ADP GlobalView</span><span class="sxs-lookup"><span data-stu-id="c9b2e-103">Tutorial: Azure Active Directory integration with ADP GlobalView</span></span>
<span data-ttu-id="c9b2e-104">The objective of this tutorial is to show you how to integrate ADP GlobalView with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c9b2e-104">The objective of this tutorial is to show you how to integrate ADP GlobalView with Azure Active Directory (Azure AD).</span></span>  

<span data-ttu-id="c9b2e-105">Integrating ADP GlobalView with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="c9b2e-105">Integrating ADP GlobalView with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="c9b2e-106">You can control in Azure AD who has access to ADP GlobalView</span><span class="sxs-lookup"><span data-stu-id="c9b2e-106">You can control in Azure AD who has access to ADP GlobalView</span></span>
* <span data-ttu-id="c9b2e-107">You can enable your users to automatically get signed-on to ADP GlobalView single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="c9b2e-107">You can enable your users to automatically get signed-on to ADP GlobalView single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="c9b2e-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="c9b2e-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="c9b2e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c9b2e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9b2e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c9b2e-110">Prerequisites</span></span>
<span data-ttu-id="c9b2e-111">To configure Azure AD integration with ADP GlobalView, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="c9b2e-111">To configure Azure AD integration with ADP GlobalView, you need the following items:</span></span>

* <span data-ttu-id="c9b2e-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="c9b2e-112">An Azure AD subscription</span></span>
* <span data-ttu-id="c9b2e-113">A ADP GlobalView SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="c9b2e-113">A ADP GlobalView SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="c9b2e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="c9b2e-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="c9b2e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="c9b2e-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="c9b2e-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c9b2e-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c9b2e-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="c9b2e-118">Scenario Description</span></span>
<span data-ttu-id="c9b2e-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>  

<span data-ttu-id="c9b2e-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="c9b2e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c9b2e-121">Adding ADP GlobalView from the gallery</span><span class="sxs-lookup"><span data-stu-id="c9b2e-121">Adding ADP GlobalView from the gallery</span></span>
2. <span data-ttu-id="c9b2e-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="c9b2e-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-adp-globalview-from-the-gallery"></a><span data-ttu-id="c9b2e-123">Add ADP GlobalView from the gallery</span><span class="sxs-lookup"><span data-stu-id="c9b2e-123">Add ADP GlobalView from the gallery</span></span>
<span data-ttu-id="c9b2e-124">To configure the integration of ADP GlobalView into Azure AD, you need to add ADP GlobalView from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-124">To configure the integration of ADP GlobalView into Azure AD, you need to add ADP GlobalView from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c9b2e-125">**To add ADP GlobalView from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c9b2e-125">**To add ADP GlobalView from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c9b2e-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="c9b2e-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="c9b2e-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="c9b2e-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="c9b2e-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="c9b2e-135">In the search box, type **ADP GlobalView**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-135">In the search box, type **ADP GlobalView**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_adpglobalview_01.png)
7. <span data-ttu-id="c9b2e-137">In the results pane, select **ADP GlobalView**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-137">In the results pane, select **ADP GlobalView**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_adpglobalview_06.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="c9b2e-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="c9b2e-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="c9b2e-140">The objective of this section is to show you how to configure and test Azure AD SSO with ADP GlobalView based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c9b2e-140">The objective of this section is to show you how to configure and test Azure AD SSO with ADP GlobalView based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c9b2e-141">For SSO to work, Azure AD needs to know what the counterpart user in ADP GlobalView to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-141">For SSO to work, Azure AD needs to know what the counterpart user in ADP GlobalView to an user in Azure AD is.</span></span> <span data-ttu-id="c9b2e-142">In other words, a link relationship between an Azure AD user and the related user in ADP GlobalView needs to be established.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-142">In other words, a link relationship between an Azure AD user and the related user in ADP GlobalView needs to be established.</span></span>  

<span data-ttu-id="c9b2e-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP GlobalView.</span></span>

<span data-ttu-id="c9b2e-144">To configure and test Azure AD SSO with ADP GlobalView, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c9b2e-144">To configure and test Azure AD SSO with ADP GlobalView, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c9b2e-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c9b2e-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c9b2e-147">**[Creating a ADP GlobalView test user](#creating-a-adp-globalview-test-user)** - to have a counterpart of Britta Simon in ADP GlobalView that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-147">**[Creating a ADP GlobalView test user](#creating-a-adp-globalview-test-user)** - to have a counterpart of Britta Simon in ADP GlobalView that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="c9b2e-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c9b2e-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="c9b2e-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="c9b2e-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="c9b2e-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your ADP GlobalView application.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your ADP GlobalView application.</span></span>

<span data-ttu-id="c9b2e-152">Your ADP GlobalView application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-152">Your ADP GlobalView application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> 

<span data-ttu-id="c9b2e-153">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-153">The following screenshot shows an example for this.</span></span> <span data-ttu-id="c9b2e-154">The claim name will always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2 which contains the EmployeeID of the user.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-154">The claim name will always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2 which contains the EmployeeID of the user.</span></span> <span data-ttu-id="c9b2e-155">Here the user mapping fron Azure AD to ADP GlobalView will be done on the EmployeeID but you can map this to a different value also based on your application settings.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-155">Here the user mapping fron Azure AD to ADP GlobalView will be done on the EmployeeID but you can map this to a different value also based on your application settings.</span></span> 

<span data-ttu-id="c9b2e-156">You can work with the ADP GlobalView team first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-156">You can work with the ADP GlobalView team first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span> <span data-ttu-id="c9b2e-157">You can also map the Email and UserID claim as shown in the picture.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-157">You can also map the Email and UserID claim as shown in the picture.</span></span>

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_adpglobalview_02.png) 

<span data-ttu-id="c9b2e-159">Before you can configure the SAML assertion, you need to contact your ADP GlobalView support team and request the value of the unique identifier attribute for your tenant.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-159">Before you can configure the SAML assertion, you need to contact your ADP GlobalView support team and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="c9b2e-160">You need this value to configure the custom claim for your application.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-160">You need this value to configure the custom claim for your application.</span></span>

<span data-ttu-id="c9b2e-161">**To configure Azure AD SSO with ADP GlobalView, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c9b2e-161">**To configure Azure AD SSO with ADP GlobalView, perform the following steps:**</span></span>

1. <span data-ttu-id="c9b2e-162">In the Azure classic portal, on the **ADP GlobalView** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-162">In the Azure classic portal, on the **ADP GlobalView** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="c9b2e-164">On the **How would you like users to sign on to ADP GlobalView** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-164">On the **How would you like users to sign on to ADP GlobalView** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_adpglobalview_03.png) 
3. <span data-ttu-id="c9b2e-166">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c9b2e-166">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_adpglobalview_04.png) 
  1. <span data-ttu-id="c9b2e-168">In the **Identifier** textbox, type the URL used to idenify ADP GlobalView application using one the following patterns: `https://<server name>.globalview.adp.com/federate2` or `https://<server name>.globalview.adp.com/federate`</span><span class="sxs-lookup"><span data-stu-id="c9b2e-168">In the **Identifier** textbox, type the URL used to idenify ADP GlobalView application using one the following patterns: `https://<server name>.globalview.adp.com/federate2` or `https://<server name>.globalview.adp.com/federate`</span></span>
  2. <span data-ttu-id="c9b2e-169">In the **Reply URL** textbox, type the URL used by Azure AD to post the response to the ADP GlobalView application, using one of the following patterns: `https://<server name>.globalview.adp.com/federate2/sp/ACS.saml2` or `https://<server name>.globalview.adp.com/federate/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="c9b2e-169">In the **Reply URL** textbox, type the URL used by Azure AD to post the response to the ADP GlobalView application, using one of the following patterns: `https://<server name>.globalview.adp.com/federate2/sp/ACS.saml2` or `https://<server name>.globalview.adp.com/federate/sp/ACS.saml2`</span></span>
  3. <span data-ttu-id="c9b2e-170">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-170">Click **Next**.</span></span>
4. <span data-ttu-id="c9b2e-171">On the **Configure single sign-on at ADP GlobalView** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c9b2e-171">On the **Configure single sign-on at ADP GlobalView** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_adpglobalview_05.png)   
  1. <span data-ttu-id="c9b2e-173">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-173">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="c9b2e-174">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-174">Click **Next**.</span></span>
5. <span data-ttu-id="c9b2e-175">To get SSO configured for your application, contact your ADP GlobalView support team and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="c9b2e-175">To get SSO configured for your application, contact your ADP GlobalView support team and provide them with the following:</span></span> 
   
   * <span data-ttu-id="c9b2e-176">The downloaded **certificate**</span><span class="sxs-lookup"><span data-stu-id="c9b2e-176">The downloaded **certificate**</span></span>
   * <span data-ttu-id="c9b2e-177">**Entity ID**</span><span class="sxs-lookup"><span data-stu-id="c9b2e-177">**Entity ID**</span></span>
   * <span data-ttu-id="c9b2e-178">**SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="c9b2e-178">**SAML SSO URL**</span></span>
   * <span data-ttu-id="c9b2e-179">**Single Sign-Out Service URL**</span><span class="sxs-lookup"><span data-stu-id="c9b2e-179">**Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="c9b2e-180">After **ADP GlobalView** team configure the instance, get the **RelayState** value from them.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-180">After **ADP GlobalView** team configure the instance, get the **RelayState** value from them.</span></span> <span data-ttu-id="c9b2e-181">Follow the below mentioned steps to configure it.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-181">Follow the below mentioned steps to configure it.</span></span> <span data-ttu-id="c9b2e-182">After this configuration you can test the integration.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-182">After this configuration you can test the integration.</span></span> <span data-ttu-id="c9b2e-183">So please note that this is important configuration for this application integration to work.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-183">So please note that this is important configuration for this application integration to work.</span></span>
    >

6. <span data-ttu-id="c9b2e-184">To configure the RelayState value in Azure AD, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c9b2e-184">To configure the RelayState value in Azure AD, perform the following steps:</span></span>   
 1. <span data-ttu-id="c9b2e-185">Logon to the [Azure Management Portal](https://portal.azure.com) as administrator.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-185">Logon to the [Azure Management Portal](https://portal.azure.com) as administrator.</span></span>
 2. <span data-ttu-id="c9b2e-186">In the left navigation pane, click **More Services**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-186">In the left navigation pane, click **More Services**.</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_adpglobalview_07.png)  
 3. <span data-ttu-id="c9b2e-188">In the **Search** textbox, type **Azure Active Directory**, and then click the related link.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-188">In the **Search** textbox, type **Azure Active Directory**, and then click the related link.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_adpglobalview_08.png)  
 4. <span data-ttu-id="c9b2e-190">Click **Enterprise Applications**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-190">Click **Enterprise Applications**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_adpglobalview_09.png) 
 5. <span data-ttu-id="c9b2e-192">In the **Manage** section, click **All Applications**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-192">In the **Manage** section, click **All Applications**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_adpglobalview_10.png) 
 6. <span data-ttu-id="c9b2e-194">In the **Search** textbox, type **ADP eTime**, and then click the related link.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-194">In the **Search** textbox, type **ADP eTime**, and then click the related link.</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_adpglobalview_11.png) 
 7. <span data-ttu-id="c9b2e-196">In the **Manage** section, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-196">In the **Manage** section, click **Single sign-on**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_adpglobalview_12.png)  
 8. <span data-ttu-id="c9b2e-198">Select **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-198">Select **Show advanced URL settings**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_adpglobalview_13.png)
 9. <span data-ttu-id="c9b2e-200">In the **Relay State** textbox, type a value using the following patterns:</span><span class="sxs-lookup"><span data-stu-id="c9b2e-200">In the **Relay State** textbox, type a value using the following patterns:</span></span>
   
    `https://<server name>.globalview.adp.com/gvolution/session/<instance name>/sso` 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_adpglobalview_14.png)  
 10. <span data-ttu-id="c9b2e-202">Save the settings.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-202">Save the settings.</span></span>
7. <span data-ttu-id="c9b2e-203">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-203">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
8. <span data-ttu-id="c9b2e-205">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-205">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c9b2e-207">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c9b2e-207">Create an Azure AD test user</span></span>
<span data-ttu-id="c9b2e-208">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-208">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

* <span data-ttu-id="c9b2e-209">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-209">In the Users list, select **Britta Simon**.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="c9b2e-211">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c9b2e-211">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c9b2e-212">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-212">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="c9b2e-214">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-214">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="c9b2e-215">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-215">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="c9b2e-217">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-217">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="c9b2e-219">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c9b2e-219">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="c9b2e-221">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-221">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="c9b2e-222">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-222">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="c9b2e-223">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-223">Click **Next**.</span></span>
6. <span data-ttu-id="c9b2e-224">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c9b2e-224">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="c9b2e-226">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-226">In the **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="c9b2e-227">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-227">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="c9b2e-228">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-228">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="c9b2e-229">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-229">In the **Role** list, select **User**.</span></span> 
 5. <span data-ttu-id="c9b2e-230">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-230">Click **Next**.</span></span>
7. <span data-ttu-id="c9b2e-231">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-231">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="c9b2e-233">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c9b2e-233">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="c9b2e-235">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-235">Write down the value of the **New Password**.</span></span>  
 2. <span data-ttu-id="c9b2e-236">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-236">Click **Complete**.</span></span>   

### <a name="create-a-adp-globalview-test-user"></a><span data-ttu-id="c9b2e-237">Create a ADP GlobalView test user</span><span class="sxs-lookup"><span data-stu-id="c9b2e-237">Create a ADP GlobalView test user</span></span>
<span data-ttu-id="c9b2e-238">The objective of this section is to create a user called Britta Simon in ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-238">The objective of this section is to create a user called Britta Simon in ADP GlobalView.</span></span> <span data-ttu-id="c9b2e-239">Please work with ADP GlobalView support team to add the users in the ADP GlobalView account.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-239">Please work with ADP GlobalView support team to add the users in the ADP GlobalView account.</span></span> 

>[!NOTE]
><span data-ttu-id="c9b2e-240">If you need to create an user manually, you need to contact the ADP GlobalView support team.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-240">If you need to create an user manually, you need to contact the ADP GlobalView support team.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c9b2e-241">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c9b2e-241">Assign the Azure AD test user</span></span>
<span data-ttu-id="c9b2e-242">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-242">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to ADP GlobalView.</span></span>

![Assign User][200] 

<span data-ttu-id="c9b2e-244">**To assign Britta Simon to ADP GlobalView, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c9b2e-244">**To assign Britta Simon to ADP GlobalView, perform the following steps:**</span></span>

1. <span data-ttu-id="c9b2e-245">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-245">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="c9b2e-247">In the applications list, select **ADP GlobalView**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-247">In the applications list, select **ADP GlobalView**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_adpglobalview_50.png) 
3. <span data-ttu-id="c9b2e-249">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-249">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="c9b2e-251">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-251">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="c9b2e-252">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-252">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="c9b2e-254">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="c9b2e-254">Test single sign-on</span></span>
<span data-ttu-id="c9b2e-255">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-255">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="c9b2e-256">When you click the ADP GlobalView tile in the Access Panel, you should get automatically signed-on to your ADP GlobalView application.</span><span class="sxs-lookup"><span data-stu-id="c9b2e-256">When you click the ADP GlobalView tile in the Access Panel, you should get automatically signed-on to your ADP GlobalView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c9b2e-257">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="c9b2e-257">Additional Resources</span></span>
* [<span data-ttu-id="c9b2e-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9b2e-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c9b2e-259">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c9b2e-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-adpglobalview-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-adpglobalview-tutorial/tutorial_general_205.png

































