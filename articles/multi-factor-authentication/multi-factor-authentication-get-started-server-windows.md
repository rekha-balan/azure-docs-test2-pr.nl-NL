---
title: Windows authentication and Azure MFA Server | Microsoft Docs
description: This is the Azure Multi-factor authentication page that will assist in deploying Windows Authentication and Azure Multi-Factor Authentication Server.
services: multi-factor-authentication
documentationcenter: ''
author: kgremban
manager: femila
editor: yossib
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/06/2017
ms.author: kgremban
ms.openlocfilehash: c6faed64553103bec161569f069392427199b271
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554778"
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a><span data-ttu-id="497a9-103">Windows Authentication and Azure Multi-Factor Authentication Server</span><span class="sxs-lookup"><span data-stu-id="497a9-103">Windows Authentication and Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="497a9-104">Use the Windows Authentication section of the Azure Multi-Factor Authentication Server to enable and configure Windows authentication for applications.</span><span class="sxs-lookup"><span data-stu-id="497a9-104">Use the Windows Authentication section of the Azure Multi-Factor Authentication Server to enable and configure Windows authentication for applications.</span></span> <span data-ttu-id="497a9-105">Before you set up Windows Authentication, keep the following list in mind:</span><span class="sxs-lookup"><span data-stu-id="497a9-105">Before you set up Windows Authentication, keep the following list in mind:</span></span>

* <span data-ttu-id="497a9-106">After setup, reboot the Azure Multi-Factor Authentication for Terminal Services to take effect.</span><span class="sxs-lookup"><span data-stu-id="497a9-106">After setup, reboot the Azure Multi-Factor Authentication for Terminal Services to take effect.</span></span>
* <span data-ttu-id="497a9-107">If ‘Require Azure Multi-Factor Authentication user match’ is checked and you are not in the user list, you will not be able to log into the machine after reboot.</span><span class="sxs-lookup"><span data-stu-id="497a9-107">If ‘Require Azure Multi-Factor Authentication user match’ is checked and you are not in the user list, you will not be able to log into the machine after reboot.</span></span>
* <span data-ttu-id="497a9-108">Trusted IPs is dependent on whether the application can provide the client IP with the authentication.</span><span class="sxs-lookup"><span data-stu-id="497a9-108">Trusted IPs is dependent on whether the application can provide the client IP with the authentication.</span></span> <span data-ttu-id="497a9-109">Currently only Terminal Services is supported.</span><span class="sxs-lookup"><span data-stu-id="497a9-109">Currently only Terminal Services is supported.</span></span>  

> [!NOTE]
> <span data-ttu-id="497a9-110">This feature is not supported to secure Terminal Services on Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="497a9-110">This feature is not supported to secure Terminal Services on Windows Server 2012 R2.</span></span>

## <a name="to-secure-an-application-with-windows-authentication-use-the-following-procedure"></a><span data-ttu-id="497a9-111">To secure an application with Windows Authentication, use the following procedure.</span><span class="sxs-lookup"><span data-stu-id="497a9-111">To secure an application with Windows Authentication, use the following procedure.</span></span>
1. <span data-ttu-id="497a9-112">In the Azure Multi-Factor Authentication Server click the Windows Authentication icon.</span><span class="sxs-lookup"><span data-stu-id="497a9-112">In the Azure Multi-Factor Authentication Server click the Windows Authentication icon.</span></span>
   <span data-ttu-id="497a9-113">![Windows Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span><span class="sxs-lookup"><span data-stu-id="497a9-113">![Windows Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span></span>
2. <span data-ttu-id="497a9-114">Check the **Enable Windows Authentication** checkbox.</span><span class="sxs-lookup"><span data-stu-id="497a9-114">Check the **Enable Windows Authentication** checkbox.</span></span> <span data-ttu-id="497a9-115">By default, this box is unchecked.</span><span class="sxs-lookup"><span data-stu-id="497a9-115">By default, this box is unchecked.</span></span>
3. <span data-ttu-id="497a9-116">The Applications tab allows the administrator to configure one or more applications for Windows Authentication.</span><span class="sxs-lookup"><span data-stu-id="497a9-116">The Applications tab allows the administrator to configure one or more applications for Windows Authentication.</span></span>
4. <span data-ttu-id="497a9-117">Select a server or application – specify whether the server/application is enabled.</span><span class="sxs-lookup"><span data-stu-id="497a9-117">Select a server or application – specify whether the server/application is enabled.</span></span> <span data-ttu-id="497a9-118">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="497a9-118">Click **OK**.</span></span>
5. <span data-ttu-id="497a9-119">Click **Add…**</span><span class="sxs-lookup"><span data-stu-id="497a9-119">Click **Add…**</span></span>
6. <span data-ttu-id="497a9-120">The Trusted IPs tab allows you to skip Azure Multi-Factor Authentication for Windows sessions originating from specific IPs.</span><span class="sxs-lookup"><span data-stu-id="497a9-120">The Trusted IPs tab allows you to skip Azure Multi-Factor Authentication for Windows sessions originating from specific IPs.</span></span> <span data-ttu-id="497a9-121">For example, if employees use the application from the office and from home, you may decide you don't want their phones ringing for Azure Multi-Factor Authentication while at the office.</span><span class="sxs-lookup"><span data-stu-id="497a9-121">For example, if employees use the application from the office and from home, you may decide you don't want their phones ringing for Azure Multi-Factor Authentication while at the office.</span></span> <span data-ttu-id="497a9-122">For this, you would specify the office subnet as Trusted IPs entry.</span><span class="sxs-lookup"><span data-stu-id="497a9-122">For this, you would specify the office subnet as Trusted IPs entry.</span></span>
7. <span data-ttu-id="497a9-123">Click **Add…**</span><span class="sxs-lookup"><span data-stu-id="497a9-123">Click **Add…**</span></span>
8. <span data-ttu-id="497a9-124">Select **Single IP** if you would like to skip a single IP address.</span><span class="sxs-lookup"><span data-stu-id="497a9-124">Select **Single IP** if you would like to skip a single IP address.</span></span>
9. <span data-ttu-id="497a9-125">Select **IP Range** if you would like to skip an entire IP range.</span><span class="sxs-lookup"><span data-stu-id="497a9-125">Select **IP Range** if you would like to skip an entire IP range.</span></span> <span data-ttu-id="497a9-126">Example 10.63.193.1-10.63.193.100.</span><span class="sxs-lookup"><span data-stu-id="497a9-126">Example 10.63.193.1-10.63.193.100.</span></span>
10. <span data-ttu-id="497a9-127">Select **Subnet** if you would like to specify a range of IPs using subnet notation.</span><span class="sxs-lookup"><span data-stu-id="497a9-127">Select **Subnet** if you would like to specify a range of IPs using subnet notation.</span></span> <span data-ttu-id="497a9-128">Enter the subnet's starting IP and pick the appropriate netmask from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="497a9-128">Enter the subnet's starting IP and pick the appropriate netmask from the drop-down list.</span></span>
11. <span data-ttu-id="497a9-129">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="497a9-129">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="497a9-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="497a9-130">Next steps</span></span>

- [<span data-ttu-id="497a9-131">Configure third-party VPN appliances for Azure MFA Server</span><span class="sxs-lookup"><span data-stu-id="497a9-131">Configure third-party VPN appliances for Azure MFA Server</span></span>](multi-factor-authentication-advanced-vpn-configurations.md)

- [<span data-ttu-id="497a9-132">Augment your existing authentication infrastructure with the NPS extension for Azure MFA</span><span class="sxs-lookup"><span data-stu-id="497a9-132">Augment your existing authentication infrastructure with the NPS extension for Azure MFA</span></span>](multi-factor-authentication-nps-extension.md)

