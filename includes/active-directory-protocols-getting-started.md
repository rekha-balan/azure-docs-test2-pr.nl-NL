---
title: Azure AD .NET Protocol Overview | Microsoft Docs
description: How to use HTTP messages to authorize access to web applications and web APIs in your tenant using Azure AD.
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/21/2016
ms.author: priyamo
ms.openlocfilehash: 42ce8dfd30cda7d4085778954350550fd9fdf13d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660462"
---
## <a name="register-your-application-with-your-ad-tenant"></a><span data-ttu-id="d1ffe-103">Register your application with your AD tenant</span><span class="sxs-lookup"><span data-stu-id="d1ffe-103">Register your application with your AD tenant</span></span>
<span data-ttu-id="d1ffe-104">First, you will need to register your application with your Azure Active Directory (Azure AD) tenant.</span><span class="sxs-lookup"><span data-stu-id="d1ffe-104">First, you will need to register your application with your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="d1ffe-105">This will give you an Application ID for your application, as well as enable it to receive tokens.</span><span class="sxs-lookup"><span data-stu-id="d1ffe-105">This will give you an Application ID for your application, as well as enable it to receive tokens.</span></span>

* <span data-ttu-id="d1ffe-106">Sign in to the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d1ffe-106">Sign in to the [Azure Portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="d1ffe-107">Choose your Azure AD tenant by clicking on your account in the top right corner of the page.</span><span class="sxs-lookup"><span data-stu-id="d1ffe-107">Choose your Azure AD tenant by clicking on your account in the top right corner of the page.</span></span>
* <span data-ttu-id="d1ffe-108">In the left hand navigation pane, click on **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d1ffe-108">In the left hand navigation pane, click on **Azure Active Directory**.</span></span>
* <span data-ttu-id="d1ffe-109">Click on **App Registrations** and click on **Add**.</span><span class="sxs-lookup"><span data-stu-id="d1ffe-109">Click on **App Registrations** and click on **Add**.</span></span>
* <span data-ttu-id="d1ffe-110">Follow the prompts and create a new application.</span><span class="sxs-lookup"><span data-stu-id="d1ffe-110">Follow the prompts and create a new application.</span></span> <span data-ttu-id="d1ffe-111">It doesn't matter if it is a web application or a native application for this tutorial, but if you'd like specific examples for web applications or native applications, check out our [quickstarts](../articles/active-directory/develop/active-directory-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="d1ffe-111">It doesn't matter if it is a web application or a native application for this tutorial, but if you'd like specific examples for web applications or native applications, check out our [quickstarts](../articles/active-directory/develop/active-directory-developers-guide.md).</span></span>
  * <span data-ttu-id="d1ffe-112">For Web Applications, provide the **Sign-On URL** which is the base URL of your app, where users can sign in e.g `http://localhost:12345`.</span><span class="sxs-lookup"><span data-stu-id="d1ffe-112">For Web Applications, provide the **Sign-On URL** which is the base URL of your app, where users can sign in e.g `http://localhost:12345`.</span></span>
<!--TODO: add once App ID URI is configurable: The **App ID URI** is a unique identifier for your application. The convention is to use `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * <span data-ttu-id="d1ffe-113">For Native Applications, provide a **Redirect URI**, which Azure AD will use to return token responses.</span><span class="sxs-lookup"><span data-stu-id="d1ffe-113">For Native Applications, provide a **Redirect URI**, which Azure AD will use to return token responses.</span></span> <span data-ttu-id="d1ffe-114">Enter a value specific to your application, .e.g `http://MyFirstAADApp`</span><span class="sxs-lookup"><span data-stu-id="d1ffe-114">Enter a value specific to your application, .e.g `http://MyFirstAADApp`</span></span>
* <span data-ttu-id="d1ffe-115">Once you've completed registration, Azure AD will assign your application a unique client identifier, the Application ID.</span><span class="sxs-lookup"><span data-stu-id="d1ffe-115">Once you've completed registration, Azure AD will assign your application a unique client identifier, the Application ID.</span></span> <span data-ttu-id="d1ffe-116">You will need this value in the next sections, so copy it from the application page.</span><span class="sxs-lookup"><span data-stu-id="d1ffe-116">You will need this value in the next sections, so copy it from the application page.</span></span>
