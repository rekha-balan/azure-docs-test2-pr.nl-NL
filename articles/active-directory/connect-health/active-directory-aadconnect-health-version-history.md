---
title: Azure AD Connect Health Version History
description: This document describes the releases for Azure AD Connect Health and what has been included in those releases.
services: active-directory
documentationcenter: ''
author: karavar
manager: samueld
editor: curtand
ms.assetid: 8dd4e998-747b-4c52-b8d3-3900fe77d88f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: billmath
ms.openlocfilehash: 35d7ac416c35c74d38f4370ee7e34a96eb18d000
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550921"
---
# <a name="azure-ad-connect-health-version-release-history"></a>Azure AD Connect Health: Version Release History
The Azure Active Directory team regularly updates Azure AD Connect Health with new features and functionality. This article lists the versions and features that have been released.

## <a name="october-2016"></a>October 2016
**Agent Update:**

* Azure AD Connect Health agent for AD FS \(version 2.6.408.0\)
  1. Improvements in detecting client IP addresses in authentication requests
  2. Bug Fixes related to Alerts
* Azure AD Connect Health agent for AD DS (version 2.6.408.0)
  1. Bug fixes related to Alerts.
* Azure AD Connect Health agent for Sync (version 2.6.353.0) released with Azure AD Connect version 1.1.281.0
  1. Provide the required data for the Synchronization Error Reports
  2. Bug fixes related to Alerts

**New preview features:**

* Synchronization Error Reports for Azure AD Connect

**New features:**

* Azure AD Connect Health for AD FS - IP address field is available in the report about top 50 users with bad username/password.

## <a name="july-2016"></a>July 2016
**New preview features:**

* [Azure AD Connect Health for AD DS](active-directory-aadconnect-health-adds.md).

## <a name="january-2016"></a>January 2016
**Agent Update:**

* Azure AD Connect Health agent for AD FS (version 2.6.91.1512)

**New features:**

* [Test Connectivity Tool for Azure AD Connect Health Agents](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service)

## <a name="november-2015"></a>November 2015
**New features:**

* Support for [Role Based Access Control](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control)

**New preview features:**

* [Azure AD Connect Health for sync](active-directory-aadconnect-health-sync.md).

**Fixed issues:**

* Bug fixes for errors seen during agent registrations.

## <a name="september-2015"></a>September 2015
**New features:**

* Wrong Username password report for AD FS
* Support to configure Unauthenticated HTTP Proxy
* Support to configure agent on Server core
* Improvements to Alerts for AD FS
* Improvements in Azure AD Connect Health Agent for AD FS for connectivity and data upload.

**Fixed issues:**

* Bug fixes in Usage Insights for AD FS Error types.

## <a name="june-2015"></a>June 2015
**Initial release of Azure AD Connect Health for AD FS and AD FS Proxy.**

**New features:**

* Alerts for monitoring AD FS and AD FS Proxy servers with email notifications.
* Easy access to AD FS topology and patterns in AD FS Performance Counters.
* Trend in successful token requests on AD FS servers grouped by Applications, Authentication Methods, Request Network Location etc.
* Trends in failed request on AD FS servers grouped by Applications, Error Types etc.
* Simpler Agent Deployment using Azure AD Global Admin credentials.  

## <a name="next-steps"></a>Next steps
Learn more about [Monitor your on-premises identity infrastructure and synchronization services in the cloud](active-directory-aadconnect-health.md).

