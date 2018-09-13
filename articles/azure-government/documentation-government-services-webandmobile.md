---
title: Azure Government Web, Mobile and API | Microsoft Docs
description: This provides a comparision of features and guidance on developing applications for Azure Government
services: azure-government
cloud: gov
documentationcenter: ''
author: brendalee
manager: zakramer
ms.assetid: a1e173a9-996a-4091-a2e3-6b1e36da9ae1
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 12/5/2016
ms.author: brendal
ms.openlocfilehash: 28aa30cd1757e8b48e099920cb3c7f6ce2df1c25
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551978"
---
# <a name="azure-government-web--mobile"></a>Azure Government Web + Mobile
## <a name="app-services"></a>App Services
### <a name="variations"></a>Variations
Azure App Services is generally available in Azure Government.

The Address for Azure App Service apps created in Azure Government is different from those created in the public cloud:

| Service Type | Azure Public | Azure Government |
| --- | --- | --- |
| App Service |*.azurewebsites.net |*.azurewebsites.us|

Some App Service features available in the public cloud are not yet available in Azure Government:

- App Service Environments
- App deployment
    - Continuous Delivery(preview)
- Settings
    - vNet integration and Hybrid connections
    - Security scanning
- Development Tools
    - Performance test
    - Resource explorer
    - PHP Debugging
- Monitoring
    - Application Insights
    - Metrics per instance
    - Live HTTP traffic
    - Application events
    - FREB logs
- Support & Troubleshooting
    - App Service Advisor
    - Failure History
    - Diagnostics as a Service
    - Mitigate


### <a name="considerations"></a>Considerations
The following information identifies the Azure Government boundary for App Service:

| Regulated/controlled data permitted | Regulated/controlled data not permitted |
| --- | --- |
| Data entered, stored, and processed within Azure App Service can contain export controlled data. Binaries running within Azure App Service. Static authenticators, such as passwords and smartcard PINs for access to Azure platform components. Private keys of certificates used to manage Azure platform components. SQL connection strings. Other security information/secrets, such as certificates, encryption keys, master keys, and storage keys stored in Azure services. |Metadata is not permitted to contain export controlled data. This metadata includes all configuration data entered when creating and maintaining your Azure App Service. Do not enter Regulated/controlled data into the following fields: Resource groups, Resource names, Resource tags|

## <a name="next-steps"></a>Next Steps
For supplemental information and updates, subscribe to the [Microsoft Azure Government Blog.](https://blogs.msdn.microsoft.com/azuregov/)

