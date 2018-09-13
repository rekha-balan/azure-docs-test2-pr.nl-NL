---
title: Threat Management for Azure B2C | Microsoft Docs
description: DOS attacks and Password Attacks detection and mitigation techniques in Azure B2C.
services: active-directory-b2c
documentationcenter: ''
author: vigunase
manager: Ajith Alexander
editor: ''
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2016
ms.author: ''
ms.openlocfilehash: 5cca5fcd445e70b4eab9197258bb783e20016f76
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554819"
---
# <a name="azure-ad-b2c-threat-management"></a>Azure AD B2C: Threat Management
Threat Management includes protection from attacks against the system and networks. Denial-of-service (DOS) can affect the availability and makes the resource unavailable to the intended users. Password attacks lead to unauthorized access to resources. Microsoft Azure Active Directory B2C has built-in features to protect your data against these threats in multiple ways. 

## <a name="denial-of-service-attack"></a>Denial of Service Attack

Azure AD B2C uses Detection and Mitigation techniques such as SYN cookies, rate and connection limits, to protect the underlying resources against these attacks.  

## <a name="password-attacks"></a>Password Attacks

Azure AD B2C also has mitigations in place for password attacks.  This technique includes both brute-force password attacks and dictionary password attacks.  Passwords set by users are required to be of reasonable complexity.  Azure AD B2C analyzes the integrity of requests to intelligently differentiate between intended users from hackers and botnets, using a various signals. B2C provides a sophisticated strategy to lock accounts based on the passwords entered, on the likelihood of an attack.

[More information on Microsoft's Threat Management](https://www.microsoft.com/trustcenter/security/threatmanagement)