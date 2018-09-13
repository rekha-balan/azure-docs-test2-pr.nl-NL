---
title: No working connector group found for an Application Proxy application | Microsoft Docs
description: Address problems you might encounter when there is no working Connector in a Connector Group for your application with the Azure AD Application Proxy
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: abcbce160205d52bcfadbfbaa1f3278b5f6c2a3e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554187"
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a>No working connector group found for an Application Proxy application

This article help you to resolve the common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.

## <a name="overview-of-steps"></a>Overview of steps
If there is no working Connector in a Connector Group for your application, there are a few ways to resolve the problem:

-   If you have no connectors in the group, you can:

    -   Download a new Connector on the right on-prem server, and assign it to this group

    -   Move an active Connector into the group

-   If you have no active connectors in the group, you can:

    -   Identify the reason your Connector is inactive and resolve

    -   Move an active Connector into the group

To know which of these is the issue, open the “Application Proxy” menu in your Application, and look at the Connector Group warning message. It specify either that the group needs at least one Connector (you have none in the group) or that it has no active Connectors (though you likely have inactive Connectors).

   ![Connector group selection in Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

For details on each of these options, see the corresponding section below. Each of these assumes that you are starting from the Connector management page. If you are looking at the error message above, you can go to this page by clicking on the warning message. Otherwise this can be found by going to **Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**

   ![Connector group management in Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a>Download a new Connector

To download a new Connector, use the “Download Connector” button at the top of the page.

note the Connector needs to be installed on a machine with direct line of sight to the backend application, and is typically placed on the same server as the application. After downloading, the Connector should appear in this menu. click the Connector, and use the “Connector Group” drop-down to make sure it belongs to the right group. Save the change.

   ![Download the connector from the Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a>Move an Active Connector

If you have an active Connector that should belong to the group and has line of sight to the target backend application, you can move the Connector into the assigned group. To do so, click the Connector. In the “Connector Group” field, use the drop-down to select the correct group, and click Save.

## <a name="resolve-an-inactive-connector"></a>Resolve an inactive Connector

If the only Connectors in the group are inactive, they are likely on a machine that does not have all the necessary ports unblocked.

see the ports Troubleshoot document for details on investigating this problem.

## <a name="next-steps"></a>Next steps
[Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md)





