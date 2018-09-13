---
title: Extensions app in Azure Active Directory B2C | Microsoft Docs
description: Restoring the b2c-extensions-app.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 9/06/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: ad3d459b1211d2777f57169f3ee896d2ab5618bc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868210"
---
# <a name="azure-ad-b2c-extensions-app"></a><span data-ttu-id="a628b-103">Azure AD B2C: Extensions app</span><span class="sxs-lookup"><span data-stu-id="a628b-103">Azure AD B2C: Extensions app</span></span>

<span data-ttu-id="a628b-104">When an Azure AD B2C directory is created, an app called `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` is automatically created inside the new directory.</span><span class="sxs-lookup"><span data-stu-id="a628b-104">When an Azure AD B2C directory is created, an app called `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` is automatically created inside the new directory.</span></span> <span data-ttu-id="a628b-105">This app, referred to as the **b2c-extensions-app**, is visible in *App registrations*.</span><span class="sxs-lookup"><span data-stu-id="a628b-105">This app, referred to as the **b2c-extensions-app**, is visible in *App registrations*.</span></span> <span data-ttu-id="a628b-106">It is used by the Azure AD B2C service to store information about users and custom attributes.</span><span class="sxs-lookup"><span data-stu-id="a628b-106">It is used by the Azure AD B2C service to store information about users and custom attributes.</span></span> <span data-ttu-id="a628b-107">If the app is deleted, Azure AD B2C will not function correctly and your production environment will be affected.</span><span class="sxs-lookup"><span data-stu-id="a628b-107">If the app is deleted, Azure AD B2C will not function correctly and your production environment will be affected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a628b-108">Do not delete the b2c-extensions-app unless you are planning to immediately delete your tenant.</span><span class="sxs-lookup"><span data-stu-id="a628b-108">Do not delete the b2c-extensions-app unless you are planning to immediately delete your tenant.</span></span> <span data-ttu-id="a628b-109">If the app remains deleted for more than 30 days, user information will be permanently lost.</span><span class="sxs-lookup"><span data-stu-id="a628b-109">If the app remains deleted for more than 30 days, user information will be permanently lost.</span></span>

## <a name="verifying-that-the-extensions-app-is-present"></a><span data-ttu-id="a628b-110">Verifying that the extensions app is present</span><span class="sxs-lookup"><span data-stu-id="a628b-110">Verifying that the extensions app is present</span></span>

<span data-ttu-id="a628b-111">To verify that the b2c-extensions-app is present:</span><span class="sxs-lookup"><span data-stu-id="a628b-111">To verify that the b2c-extensions-app is present:</span></span>

1. <span data-ttu-id="a628b-112">Inside your Azure AD B2C tenant, click on **All services** in the left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a628b-112">Inside your Azure AD B2C tenant, click on **All services** in the left-hand navigation menu.</span></span>
1. <span data-ttu-id="a628b-113">Search for and open **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="a628b-113">Search for and open **App registrations**.</span></span>
1. <span data-ttu-id="a628b-114">Look for an app that begins with **b2c-extensions-app**</span><span class="sxs-lookup"><span data-stu-id="a628b-114">Look for an app that begins with **b2c-extensions-app**</span></span>

## <a name="recover-the-extensions-app"></a><span data-ttu-id="a628b-115">Recover the extensions app</span><span class="sxs-lookup"><span data-stu-id="a628b-115">Recover the extensions app</span></span>

<span data-ttu-id="a628b-116">If you accidentally deleted the b2c-extensions-app, you have 30 days to recover it.</span><span class="sxs-lookup"><span data-stu-id="a628b-116">If you accidentally deleted the b2c-extensions-app, you have 30 days to recover it.</span></span> <span data-ttu-id="a628b-117">You can restore the app using the Graph API:</span><span class="sxs-lookup"><span data-stu-id="a628b-117">You can restore the app using the Graph API:</span></span>

1. <span data-ttu-id="a628b-118">Browse to [https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="a628b-118">Browse to [https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span></span>
1. <span data-ttu-id="a628b-119">Log in to the site as a global administrator for the Azure AD B2C directory that you want to restore the deleted app for.</span><span class="sxs-lookup"><span data-stu-id="a628b-119">Log in to the site as a global administrator for the Azure AD B2C directory that you want to restore the deleted app for.</span></span> <span data-ttu-id="a628b-120">This global administrator must have an email address similar to the following: `username@{yourTenant}.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="a628b-120">This global administrator must have an email address similar to the following: `username@{yourTenant}.onmicrosoft.com`.</span></span>
1. <span data-ttu-id="a628b-121">Issue an HTTP GET against the URL `https://graph.windows.net/myorganization/deletedApplications` with api-version=1.6.</span><span class="sxs-lookup"><span data-stu-id="a628b-121">Issue an HTTP GET against the URL `https://graph.windows.net/myorganization/deletedApplications` with api-version=1.6.</span></span> <span data-ttu-id="a628b-122">This operation will list all of the applications that have been deleted within the past 30 days.</span><span class="sxs-lookup"><span data-stu-id="a628b-122">This operation will list all of the applications that have been deleted within the past 30 days.</span></span>
1. <span data-ttu-id="a628b-123">Find the application in the list where the name begins with 'b2c-extension-app’ and copy its `objectid` property value.</span><span class="sxs-lookup"><span data-stu-id="a628b-123">Find the application in the list where the name begins with 'b2c-extension-app’ and copy its `objectid` property value.</span></span>
1. <span data-ttu-id="a628b-124">Issue an HTTP POST against the URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span><span class="sxs-lookup"><span data-stu-id="a628b-124">Issue an HTTP POST against the URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span></span> <span data-ttu-id="a628b-125">Replace the `{OBJECTID}` portion of the URL with the `objectid` from the previous step.</span><span class="sxs-lookup"><span data-stu-id="a628b-125">Replace the `{OBJECTID}` portion of the URL with the `objectid` from the previous step.</span></span> 

<span data-ttu-id="a628b-126">You should now be able to [see the restored app](#verifying-that-the-extensions-app-is-present) in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a628b-126">You should now be able to [see the restored app](#verifying-that-the-extensions-app-is-present) in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="a628b-127">An application can only be restored if it has been deleted within the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="a628b-127">An application can only be restored if it has been deleted within the last 30 days.</span></span> <span data-ttu-id="a628b-128">If it has been more than 30 days, data will be permanently lost.</span><span class="sxs-lookup"><span data-stu-id="a628b-128">If it has been more than 30 days, data will be permanently lost.</span></span> <span data-ttu-id="a628b-129">For more assistance, file a support ticket.</span><span class="sxs-lookup"><span data-stu-id="a628b-129">For more assistance, file a support ticket.</span></span>