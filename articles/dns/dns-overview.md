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
# <a name="azure-dns-overview"></a>Azure DNS Overview

The Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name to its IP address. Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure. By hosting your domains in Azure, you can manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services.

DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers. We use Anycast networking so that each DNS query is answered by the closest available DNS server. This provides both fast performance and high availability for your domain.

The Azure DNS service is based on Azure Resource Manager. As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking. Your domains and records can be managed via the Azure portal, Azure PowerShell cmdlets, and the cross-platform Azure CLI. Applications requiring automatic DNS management can integrate with the service via the REST API and SDKs.

Azure DNS does not currently support purchasing of domain names. If you want to purchase domains, you need to use a third-party domain name registrar. The registrar typically charges a small annual fee. The domains can then be hosted in Azure DNS for management of DNS records. See [Delegate a Domain to Azure DNS](dns-domain-delegation.md) for details.

### <a name="next-steps"></a>Next steps

[Create a DNS zone](./dns-getstarted-create-dnszone-portal.md)

