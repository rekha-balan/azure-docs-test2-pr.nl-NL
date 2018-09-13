---
title: Connect domain-joined devices to Azure AD for Windows 10 experiences | Microsoft Docs
description: Explains how administrators can configure Group Policy to enable devices to be domain-joined to the enterprise network.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
editor: ''
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: markvi
ms.openlocfilehash: 39bd4fcbe1b9a197bcf5b8bb33bf6fffae2063fc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551462"
---
# <a name="connect-domain-joined-devices-to-azure-ad-for-windows-10-experiences"></a><span data-ttu-id="9c662-103">Connect domain-joined devices to Azure AD for Windows 10 experiences</span><span class="sxs-lookup"><span data-stu-id="9c662-103">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>
<span data-ttu-id="9c662-104">Domain join is the traditional way organizations have connected devices for work for the last 15 years and more.</span><span class="sxs-lookup"><span data-stu-id="9c662-104">Domain join is the traditional way organizations have connected devices for work for the last 15 years and more.</span></span> <span data-ttu-id="9c662-105">It has enabled users to sign in to their devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT to fully manage these devices.</span><span class="sxs-lookup"><span data-stu-id="9c662-105">It has enabled users to sign in to their devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT to fully manage these devices.</span></span> <span data-ttu-id="9c662-106">Organizations typically rely on imaging methods to provision devices to users and generally use System Center Configuration Manager (SCCM) or Group Policy to manage them.</span><span class="sxs-lookup"><span data-stu-id="9c662-106">Organizations typically rely on imaging methods to provision devices to users and generally use System Center Configuration Manager (SCCM) or Group Policy to manage them.</span></span>


<span data-ttu-id="9c662-107">Domain join in Windows 10 provides you with the following benefits after you connect devices to Azure Active Directory (Azure AD):</span><span class="sxs-lookup"><span data-stu-id="9c662-107">Domain join in Windows 10 provides you with the following benefits after you connect devices to Azure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="9c662-108">Single sign-on (SSO) to Azure AD resources from anywhere</span><span class="sxs-lookup"><span data-stu-id="9c662-108">Single sign-on (SSO) to Azure AD resources from anywhere</span></span>
* <span data-ttu-id="9c662-109">Access to the enterprise Windows Store by using work or school accounts (no Microsoft account required)</span><span class="sxs-lookup"><span data-stu-id="9c662-109">Access to the enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="9c662-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span><span class="sxs-lookup"><span data-stu-id="9c662-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="9c662-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span><span class="sxs-lookup"><span data-stu-id="9c662-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="9c662-112">Ability to restrict access only to devices that comply with organizational device Group Policy settings</span><span class="sxs-lookup"><span data-stu-id="9c662-112">Ability to restrict access only to devices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c662-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9c662-113">Prerequisites</span></span>
<span data-ttu-id="9c662-114">Domain join continues to be useful.</span><span class="sxs-lookup"><span data-stu-id="9c662-114">Domain join continues to be useful.</span></span> <span data-ttu-id="9c662-115">However, to get the Azure AD benefits of SSO, roaming of settings with work or school accounts, and access to Windows Store with work or school accounts, you will need the following:</span><span class="sxs-lookup"><span data-stu-id="9c662-115">However, to get the Azure AD benefits of SSO, roaming of settings with work or school accounts, and access to Windows Store with work or school accounts, you will need the following:</span></span>

* <span data-ttu-id="9c662-116">Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="9c662-116">Azure AD subscription</span></span>
* <span data-ttu-id="9c662-117">Azure AD Connect to extend the on-premises directory to Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c662-117">Azure AD Connect to extend the on-premises directory to Azure AD</span></span>
* <span data-ttu-id="9c662-118">Policy that's set to connect domain-joined devices to Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c662-118">Policy that's set to connect domain-joined devices to Azure AD</span></span>
* <span data-ttu-id="9c662-119">Windows 10 build (build 10551 or newer) for devices</span><span class="sxs-lookup"><span data-stu-id="9c662-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="9c662-120">To enable Windows Hello for Business and Windows Hello, you will also need the following:</span><span class="sxs-lookup"><span data-stu-id="9c662-120">To enable Windows Hello for Business and Windows Hello, you will also need the following:</span></span>

- <span data-ttu-id="9c662-121">**Public key infrastructure (PKI)** for user certificates issuance.</span><span class="sxs-lookup"><span data-stu-id="9c662-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="9c662-122">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span><span class="sxs-lookup"><span data-stu-id="9c662-122">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span></span>  
<span data-ttu-id="9c662-123">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="9c662-123">For more information, see:</span></span> 
    - [<span data-ttu-id="9c662-124">Documentation for System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="9c662-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="9c662-125">System Center Configuration Manager Team Blog</span><span class="sxs-lookup"><span data-stu-id="9c662-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="9c662-126">Windows Hello for Business settings in System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="9c662-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="9c662-127">As an alternative to the PKI deployment requirement, you can do the following:</span><span class="sxs-lookup"><span data-stu-id="9c662-127">As an alternative to the PKI deployment requirement, you can do the following:</span></span>

* <span data-ttu-id="9c662-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="9c662-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="9c662-129">To enable conditional access, you can create Group Policy settings that allow access to domain-joined devices with no additional deployments.</span><span class="sxs-lookup"><span data-stu-id="9c662-129">To enable conditional access, you can create Group Policy settings that allow access to domain-joined devices with no additional deployments.</span></span> <span data-ttu-id="9c662-130">To manage access control based on compliance of the device, you will need the following:</span><span class="sxs-lookup"><span data-stu-id="9c662-130">To manage access control based on compliance of the device, you will need the following:</span></span>

* <span data-ttu-id="9c662-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span><span class="sxs-lookup"><span data-stu-id="9c662-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="9c662-132">Deployment instructions</span><span class="sxs-lookup"><span data-stu-id="9c662-132">Deployment instructions</span></span>

<span data-ttu-id="9c662-133">To deploy, follow the steps listed in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="9c662-133">To deploy, follow the steps listed in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="9c662-134">Next step</span><span class="sxs-lookup"><span data-stu-id="9c662-134">Next step</span></span>
* [<span data-ttu-id="9c662-135">Windows 10 for the enterprise: Ways to use devices for work</span><span class="sxs-lookup"><span data-stu-id="9c662-135">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="9c662-136">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="9c662-136">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="9c662-137">Learn about usage scenarios for Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="9c662-137">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="9c662-138">Connect domain-joined devices to Azure AD for Windows 10 experiences</span><span class="sxs-lookup"><span data-stu-id="9c662-138">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="9c662-139">Set up Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="9c662-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

