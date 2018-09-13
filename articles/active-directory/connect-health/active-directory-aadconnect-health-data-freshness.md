---
title: Azure AD Connect Health - Health service data is not up to date alert | Microsoft Docs
description: This document describes the cause of "Health service data is not up to date" alert and how to troubleshoot it.
services: active-directory
documentationcenter: ''
author: zhiweiw
manager: maheshu
editor: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2018
ms.author: zhiweiw
ms.openlocfilehash: 45e88320a64770239c8f322212e12ca7826cd0da
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856487"
---
# <a name="health-service-data-is-not-up-to-date-alert"></a>Health service data is not up to date alert

## <a name="overview"></a>Overview
<li>Azure AD Connect Health generates data fresh alert when it does not receive all the data points from the server for two hours. The alert title is **Health service data is not up to date**. </li>
<li>The **Warning** status alert fires if Connect Health does not receive partial data elements sent from server for two hours. Warning status alert does not trigger email notifications to the tenant admin. </li>
<li>The **Error** status alert fires if Connect Health does not receive any data elements sent from server for two hours. Error status alert triggers email notifications to the tenant admin. </li>

>[!IMPORTANT] 
> This alert follows Connect Health [data retention policy](active-directory-aadconnect-health-gdpr.md#data-retention-policy)

## <a name="troubleshooting-steps"></a>Troubleshooting steps 
* Make sure to go over and meet the [requirements section](active-directory-aadconnect-health-agent-install.md#requirements).
* Use [test connectivity tool](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service) to discover connectivity issues.


## <a name="next-steps"></a>Next steps
* [Azure AD Connect Health FAQ](active-directory-aadconnect-health-faq.md)
