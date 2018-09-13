---
title: "Troubleshooting: 'Active Directory' item is missing or not available | Microsoft Docs"
description: What to do when Active Directory menu item doesn't appear in the Azure Management Portal.
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: ''
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 01/07/2017
ms.author: mbaldwin
ms.openlocfilehash: f5a34ac7674ddb3c224e5b05dfdbea4df8ed5776
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670447"
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a><span data-ttu-id="b617e-103">Troubleshooting: 'Active Directory' item is missing or not available</span><span class="sxs-lookup"><span data-stu-id="b617e-103">Troubleshooting: 'Active Directory' item is missing or not available</span></span>
<span data-ttu-id="b617e-104">Many of the instructions for using Azure Active Directory features and services begin with "Go to the Azure Management Portal and click **Active Directory**."</span><span class="sxs-lookup"><span data-stu-id="b617e-104">Many of the instructions for using Azure Active Directory features and services begin with "Go to the Azure Management Portal and click **Active Directory**."</span></span> <span data-ttu-id="b617e-105">But what do you do if the Active Directory extension or menu item does not appear or if it is marked **Not Available**?</span><span class="sxs-lookup"><span data-stu-id="b617e-105">But what do you do if the Active Directory extension or menu item does not appear or if it is marked **Not Available**?</span></span> <span data-ttu-id="b617e-106">This topic is designed to help.</span><span class="sxs-lookup"><span data-stu-id="b617e-106">This topic is designed to help.</span></span> <span data-ttu-id="b617e-107">It describes the conditions under which **Active Directory** does not appear or is unavailable and explains how to proceed.</span><span class="sxs-lookup"><span data-stu-id="b617e-107">It describes the conditions under which **Active Directory** does not appear or is unavailable and explains how to proceed.</span></span>

## <a name="active-directory-is-missing"></a><span data-ttu-id="b617e-108">Active Directory is missing</span><span class="sxs-lookup"><span data-stu-id="b617e-108">Active Directory is missing</span></span>
<span data-ttu-id="b617e-109">Typically, an **Active Directory** item appears in the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="b617e-109">Typically, an **Active Directory** item appears in the left navigation menu.</span></span> <span data-ttu-id="b617e-110">The instructions in Azure Active Directory procedures assume that this item is in your view.</span><span class="sxs-lookup"><span data-stu-id="b617e-110">The instructions in Azure Active Directory procedures assume that this item is in your view.</span></span>

![Screen shot: Active Directory in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-troubleshooting/typical-view.png)

<span data-ttu-id="b617e-112">The Active Directory item appears in the left navigation menu when any of the following conditions is true.</span><span class="sxs-lookup"><span data-stu-id="b617e-112">The Active Directory item appears in the left navigation menu when any of the following conditions is true.</span></span> <span data-ttu-id="b617e-113">Otherwise, the item does not appear.</span><span class="sxs-lookup"><span data-stu-id="b617e-113">Otherwise, the item does not appear.</span></span>

* <span data-ttu-id="b617e-114">The current user signed on with a Microsoft account (formerly known as a Windows Live ID).</span><span class="sxs-lookup"><span data-stu-id="b617e-114">The current user signed on with a Microsoft account (formerly known as a Windows Live ID).</span></span>
  
    <span data-ttu-id="b617e-115">OR</span><span class="sxs-lookup"><span data-stu-id="b617e-115">OR</span></span>
* <span data-ttu-id="b617e-116">The Azure tenant has a directory and the current account is a directory administrator.</span><span class="sxs-lookup"><span data-stu-id="b617e-116">The Azure tenant has a directory and the current account is a directory administrator.</span></span>
  
    <span data-ttu-id="b617e-117">OR</span><span class="sxs-lookup"><span data-stu-id="b617e-117">OR</span></span>
* <span data-ttu-id="b617e-118">The Azure tenant has at least one Azure AD Access Control (ACS) namespace.</span><span class="sxs-lookup"><span data-stu-id="b617e-118">The Azure tenant has at least one Azure AD Access Control (ACS) namespace.</span></span> <span data-ttu-id="b617e-119">For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span><span class="sxs-lookup"><span data-stu-id="b617e-119">For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span></span>
  
    <span data-ttu-id="b617e-120">OR</span><span class="sxs-lookup"><span data-stu-id="b617e-120">OR</span></span>
* <span data-ttu-id="b617e-121">The Azure tenant has at least one Azure Multi-Factor Authentication provider.</span><span class="sxs-lookup"><span data-stu-id="b617e-121">The Azure tenant has at least one Azure Multi-Factor Authentication provider.</span></span> <span data-ttu-id="b617e-122">For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="b617e-122">For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>

<span data-ttu-id="b617e-123">To create an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b617e-123">To create an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.</span></span>

<span data-ttu-id="b617e-124">To get administrative rights to a directory, have an administrator assign an administrator role to your account.</span><span class="sxs-lookup"><span data-stu-id="b617e-124">To get administrative rights to a directory, have an administrator assign an administrator role to your account.</span></span> <span data-ttu-id="b617e-125">For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="b617e-125">For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).</span></span>

## <a name="active-directory-is-not-available"></a><span data-ttu-id="b617e-126">Active Directory is not available</span><span class="sxs-lookup"><span data-stu-id="b617e-126">Active Directory is not available</span></span>
<span data-ttu-id="b617e-127">When you click **+New** > **App Services**, an **Active Directory** item appears.</span><span class="sxs-lookup"><span data-stu-id="b617e-127">When you click **+New** > **App Services**, an **Active Directory** item appears.</span></span> <span data-ttu-id="b617e-128">Specifically, the Active Directory item appears when any of the Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available to the current user.</span><span class="sxs-lookup"><span data-stu-id="b617e-128">Specifically, the Active Directory item appears when any of the Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available to the current user.</span></span>

<span data-ttu-id="b617e-129">However, while the page is loading, the item is dimmed and is marked **Not Available**.</span><span class="sxs-lookup"><span data-stu-id="b617e-129">However, while the page is loading, the item is dimmed and is marked **Not Available**.</span></span> <span data-ttu-id="b617e-130">This is a temporary state.</span><span class="sxs-lookup"><span data-stu-id="b617e-130">This is a temporary state.</span></span> <span data-ttu-id="b617e-131">If you wait a few seconds, the item becomes available.</span><span class="sxs-lookup"><span data-stu-id="b617e-131">If you wait a few seconds, the item becomes available.</span></span> <span data-ttu-id="b617e-132">If the delay is prolonged, refreshing the web page often resolves the problem.</span><span class="sxs-lookup"><span data-stu-id="b617e-132">If the delay is prolonged, refreshing the web page often resolves the problem.</span></span>

![Screen shot: Active Directory is not available](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-troubleshooting/not-available.png)



