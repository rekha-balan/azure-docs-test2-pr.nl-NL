---
title: How to get an Azure AD tenant | Microsoft Docs
description: How to get an Azure Active Directory tenant for registering and building applications.
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: 1f4b24eb-ab4d-4baa-a717-2a0e5b8d27cd
ms.service: active-directory
ms.component: develop
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2018
ms.author: celested
ms.custom: aaddev
ms.openlocfilehash: 1f866d3ee56b0c9a1e7a986d3ac951764b6a1cae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856978"
---
# <a name="how-to-get-an-azure-active-directory-tenant"></a><span data-ttu-id="bc6c8-103">How to get an Azure Active Directory tenant</span><span class="sxs-lookup"><span data-stu-id="bc6c8-103">How to get an Azure Active Directory tenant</span></span>

<span data-ttu-id="bc6c8-104">In Azure Active Directory (Azure AD), a [tenant](https://msdn.microsoft.com/library/azure/jj573650.aspx#Anchor_0) is representative of an organization.</span><span class="sxs-lookup"><span data-stu-id="bc6c8-104">In Azure Active Directory (Azure AD), a [tenant](https://msdn.microsoft.com/library/azure/jj573650.aspx#Anchor_0) is representative of an organization.</span></span> <span data-ttu-id="bc6c8-105">It is a dedicated instance of the Azure AD service that an organization receives and owns when it creates a relationship with Microsoft, such as by signing up for a Microsoft cloud service like Azure, Microsoft Intune, or Office 365.</span><span class="sxs-lookup"><span data-stu-id="bc6c8-105">It is a dedicated instance of the Azure AD service that an organization receives and owns when it creates a relationship with Microsoft, such as by signing up for a Microsoft cloud service like Azure, Microsoft Intune, or Office 365.</span></span> <span data-ttu-id="bc6c8-106">Each Azure AD tenant is distinct and separate from other Azure AD tenants.</span><span class="sxs-lookup"><span data-stu-id="bc6c8-106">Each Azure AD tenant is distinct and separate from other Azure AD tenants.</span></span> 

<span data-ttu-id="bc6c8-107">A tenant houses the users in a company and the information about them--their passwords, user profile data, permissions, and so on.</span><span class="sxs-lookup"><span data-stu-id="bc6c8-107">A tenant houses the users in a company and the information about them--their passwords, user profile data, permissions, and so on.</span></span> <span data-ttu-id="bc6c8-108">It also contains groups, applications, and other information pertaining to an organization and its security.</span><span class="sxs-lookup"><span data-stu-id="bc6c8-108">It also contains groups, applications, and other information pertaining to an organization and its security.</span></span>

<span data-ttu-id="bc6c8-109">To allow Azure AD users to sign in to your application, you must register your application in a tenant of your own.</span><span class="sxs-lookup"><span data-stu-id="bc6c8-109">To allow Azure AD users to sign in to your application, you must register your application in a tenant of your own.</span></span> <span data-ttu-id="bc6c8-110">Creating an Azure AD tenant and publishing an application in it is **absolutely free** although you can choose to pay for premium features in your tenant.</span><span class="sxs-lookup"><span data-stu-id="bc6c8-110">Creating an Azure AD tenant and publishing an application in it is **absolutely free** although you can choose to pay for premium features in your tenant.</span></span> <span data-ttu-id="bc6c8-111">In fact, many developers create several tenants and applications for experimentation, development, staging, and testing purposes.</span><span class="sxs-lookup"><span data-stu-id="bc6c8-111">In fact, many developers create several tenants and applications for experimentation, development, staging, and testing purposes.</span></span>

## <a name="use-an-existing-azure-ad-tenant"></a><span data-ttu-id="bc6c8-112">Use an existing Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="bc6c8-112">Use an existing Azure AD tenant</span></span>

<span data-ttu-id="bc6c8-113">Many developers already have tenants through services or subscriptions that are tied to Azure AD tenants such as Office 365 or Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="bc6c8-113">Many developers already have tenants through services or subscriptions that are tied to Azure AD tenants such as Office 365 or Azure subscriptions.</span></span> <span data-ttu-id="bc6c8-114">To check if you already have a tenant, sign in to the [Azure portal](https://portal.azure.com) with the account you want to use to manage your application and check the upper right corner where your account information is shown.</span><span class="sxs-lookup"><span data-stu-id="bc6c8-114">To check if you already have a tenant, sign in to the [Azure portal](https://portal.azure.com) with the account you want to use to manage your application and check the upper right corner where your account information is shown.</span></span> <span data-ttu-id="bc6c8-115">If you have a tenant, you'll automatically be logged into it and you'll see the tenant name directly under your account name.</span><span class="sxs-lookup"><span data-stu-id="bc6c8-115">If you have a tenant, you'll automatically be logged into it and you'll see the tenant name directly under your account name.</span></span> <span data-ttu-id="bc6c8-116">If you hover over your account name on the upper right-hand side of the Azure portal, you will see your name, email, directory and tenant ID (a GUID), and your domain.</span><span class="sxs-lookup"><span data-stu-id="bc6c8-116">If you hover over your account name on the upper right-hand side of the Azure portal, you will see your name, email, directory and tenant ID (a GUID), and your domain.</span></span> <span data-ttu-id="bc6c8-117">If your account is associated with multiple tenants, you can select your account name to open a menu where you can switch between tenants.</span><span class="sxs-lookup"><span data-stu-id="bc6c8-117">If your account is associated with multiple tenants, you can select your account name to open a menu where you can switch between tenants.</span></span> <span data-ttu-id="bc6c8-118">Each tenant has its own tenant ID.</span><span class="sxs-lookup"><span data-stu-id="bc6c8-118">Each tenant has its own tenant ID.</span></span>

> [!TIP]
> <span data-ttu-id="bc6c8-119">If you need to find the tenant ID, there are multiple ways to find this info.</span><span class="sxs-lookup"><span data-stu-id="bc6c8-119">If you need to find the tenant ID, there are multiple ways to find this info.</span></span> <span data-ttu-id="bc6c8-120">You can hover over your account name to get the tenant ID or you can select **Azure Active Directory > Properties > Directory ID** in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bc6c8-120">You can hover over your account name to get the tenant ID or you can select **Azure Active Directory > Properties > Directory ID** in the Azure portal.</span></span>

<span data-ttu-id="bc6c8-121">If you don't have an existing tenant associated with your account, you'll see a GUID under your account name and you will not be able to perform actions like registering apps until you [create a new tenant](#create-a-new-azure-ad-tenant).</span><span class="sxs-lookup"><span data-stu-id="bc6c8-121">If you don't have an existing tenant associated with your account, you'll see a GUID under your account name and you will not be able to perform actions like registering apps until you [create a new tenant](#create-a-new-azure-ad-tenant).</span></span>

## <a name="create-a-new-azure-ad-tenant"></a><span data-ttu-id="bc6c8-122">Create a new Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="bc6c8-122">Create a new Azure AD tenant</span></span>

<span data-ttu-id="bc6c8-123">If you don't already have an Azure AD tenant or want to create a new one, you can do so using the [directory creation experience](https://portal.azure.com/#create/Microsoft.AzureActiveDirectory) in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bc6c8-123">If you don't already have an Azure AD tenant or want to create a new one, you can do so using the [directory creation experience](https://portal.azure.com/#create/Microsoft.AzureActiveDirectory) in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bc6c8-124">The process will take about a minute, and in the end you'll be prompted to navigate to your newly created tenant.</span><span class="sxs-lookup"><span data-stu-id="bc6c8-124">The process will take about a minute, and in the end you'll be prompted to navigate to your newly created tenant.</span></span>
