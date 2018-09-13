---
title: Overview of Azure DNS | Microsoft Docs
description: Overview of DNS hosting service on Microsoft Azure. Host your domain on Microsoft Azure.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: gwallace
ms.openlocfilehash: f8ccf5c0fab1e4aca85b22b99a1a5b48f35dfcbc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661210"
---
# <a name="azure-dns-overview"></a><span data-ttu-id="1d234-104">Azure DNS Overview</span><span class="sxs-lookup"><span data-stu-id="1d234-104">Azure DNS Overview</span></span>

<span data-ttu-id="1d234-105">The Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name to its IP address.</span><span class="sxs-lookup"><span data-stu-id="1d234-105">The Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name to its IP address.</span></span> <span data-ttu-id="1d234-106">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span><span class="sxs-lookup"><span data-stu-id="1d234-106">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="1d234-107">By hosting your domains in Azure, you can manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services.</span><span class="sxs-lookup"><span data-stu-id="1d234-107">By hosting your domains in Azure, you can manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services.</span></span>

<span data-ttu-id="1d234-108">DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span><span class="sxs-lookup"><span data-stu-id="1d234-108">DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="1d234-109">We use Anycast networking so that each DNS query is answered by the closest available DNS server.</span><span class="sxs-lookup"><span data-stu-id="1d234-109">We use Anycast networking so that each DNS query is answered by the closest available DNS server.</span></span> <span data-ttu-id="1d234-110">This provides both fast performance and high availability for your domain.</span><span class="sxs-lookup"><span data-stu-id="1d234-110">This provides both fast performance and high availability for your domain.</span></span>

<span data-ttu-id="1d234-111">The Azure DNS service is based on Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1d234-111">The Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="1d234-112">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span><span class="sxs-lookup"><span data-stu-id="1d234-112">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="1d234-113">Your domains and records can be managed via the Azure portal, Azure PowerShell cmdlets, and the cross-platform Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="1d234-113">Your domains and records can be managed via the Azure portal, Azure PowerShell cmdlets, and the cross-platform Azure CLI.</span></span> <span data-ttu-id="1d234-114">Applications requiring automatic DNS management can integrate with the service via the REST API and SDKs.</span><span class="sxs-lookup"><span data-stu-id="1d234-114">Applications requiring automatic DNS management can integrate with the service via the REST API and SDKs.</span></span>

<span data-ttu-id="1d234-115">Azure DNS does not currently support purchasing of domain names.</span><span class="sxs-lookup"><span data-stu-id="1d234-115">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="1d234-116">If you want to purchase domains, you need to use a third-party domain name registrar.</span><span class="sxs-lookup"><span data-stu-id="1d234-116">If you want to purchase domains, you need to use a third-party domain name registrar.</span></span> <span data-ttu-id="1d234-117">The registrar typically charges a small annual fee.</span><span class="sxs-lookup"><span data-stu-id="1d234-117">The registrar typically charges a small annual fee.</span></span> <span data-ttu-id="1d234-118">The domains can then be hosted in Azure DNS for management of DNS records.</span><span class="sxs-lookup"><span data-stu-id="1d234-118">The domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="1d234-119">See [Delegate a Domain to Azure DNS](dns-domain-delegation.md) for details.</span><span class="sxs-lookup"><span data-stu-id="1d234-119">See [Delegate a Domain to Azure DNS](dns-domain-delegation.md) for details.</span></span>

### <a name="next-steps"></a><span data-ttu-id="1d234-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="1d234-120">Next steps</span></span>

[<span data-ttu-id="1d234-121">Create a DNS zone</span><span class="sxs-lookup"><span data-stu-id="1d234-121">Create a DNS zone</span></span>](./dns-getstarted-create-dnszone-portal.md)

