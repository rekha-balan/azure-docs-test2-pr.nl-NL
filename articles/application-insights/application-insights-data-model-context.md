---
title: Azure Application Insights Telemetry Data Model - Telemetry Context | Microsoft Docs
description: Application Insights telemetry context data model
services: application-insights
documentationcenter: .net
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: conceptual
ms.date: 05/15/2017
ms.reviewer: sergkanz
ms.author: mbullwin
ms.openlocfilehash: b6cfae20f09b19a57cf411777e78abb1dbbf0484
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855935"
---
# <a name="telemetry-context-application-insights-data-model"></a>Telemetry context: Application Insights data model

Every telemetry item may have a strongly typed context fields. Every field enables a specific monitoring scenario. Use the custom properties collection to store custom or application-specific contextual information.


## <a name="application-version"></a>Application version

Information in the application context fields is always about the application that is sending the telemetry. Application version is used to analyze trend changes in the application behavior and its correlation to the deployments.

Max length: 1024


## <a name="client-ip-address"></a>Client IP address

The IP address of the client device. IPv4 and IPv6 are supported. When telemetry is sent from a service, the location context is about the user that initiated the operation in the service. Application Insights extract the geo-location information from the client IP and then truncate it. So client IP by itself cannot be used as end-user identifiable information. 

Max length: 46


## <a name="device-type"></a>Device type

Originally this field was used to indicate the type of the device the end user of the application is using. Today used primarily to distinguish JavaScript telemetry with the device type 'Browser' from server-side telemetry with the device type 'PC'.

Max length: 64


## <a name="operation-id"></a>Operation id

A unique identifier of the root operation. This identifier allows to group telemetry across multiple components. See [telemetry correlation](application-insights-correlation.md) for details. The operation id is created by either a request or a page view. All other telemetry sets this field to the value for the containing request or page view. 

Max length: 128


## <a name="parent-operation-id"></a>Parent operation ID

The unique identifier of the telemetry item's immediate parent. See [telemetry correlation](application-insights-correlation.md) for details.

Max length: 128


## <a name="operation-name"></a>Operation name

The name (group) of the operation. The operation name is created by either a request or a page view. All other telemetry items set this field to the value for the containing request or page view. Operation name is used for finding all the telemetry items for a group of operations (for example 'GET Home/Index'). This context property is used to answer questions like "what are the typical exceptions thrown on this page."

Max length: 1024


## <a name="synthetic-source-of-the-operation"></a>Synthetic source of the operation

Name of synthetic source. Some telemetry from the application may represent synthetic traffic. It may be web crawler indexing the web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.

Max length: 1024


## <a name="session-id"></a>Session id

Session ID - the instance of the user's interaction with the app. Information in the session context fields is always about the end user. When telemetry is sent from a service, the session context is about the user that initiated the operation in the service.

Max length: 64


## <a name="anonymous-user-id"></a>Anonymous user id

Anonymous user id. Represents the end user of the application. When telemetry is sent from a service, the user context is about the user that initiated the operation in the service.

[Sampling](app-insights-sampling.md) is one of the techniques to minimize the amount of collected telemetry. Sampling algorithm attempts to either sample in or out all the correlated telemetry. Anonymous user id is used for sampling score generation. So anonymous user id should be a random enough value. 

Using anonymous user id to store user name is a misuse of the field. Use Authenticated user id.

Max length: 128


## <a name="authenticated-user-id"></a>Authenticated user id

Authenticated user id. The opposite of anonymous user id, this field represents the user with a friendly name. Since its PII information it is not collected by default by most SDK.

Max length: 1024


## <a name="account-id"></a>Account id

In multi-tenant applications this is the account ID or name, which the user is acting with. Examples may be subscription ID for Azure portal or blog name blogging platform.

Max length: 1024


## <a name="cloud-role"></a>Cloud role

Name of the role the application is a part of. Maps directly to the role name in azure. Can also be used to distinguish micro services, which are part of a single application.

Max length: 256


## <a name="cloud-role-instance"></a>Cloud role instance

Name of the instance where the application is running. Computer name for on-premises, instance name for Azure.

Max length: 256


## <a name="internal-sdk-version"></a>Internal: SDK version

SDK version. See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.

Max length: 64


## <a name="internal-node-name"></a>Internal: Node name

This field represents the node name used for billing purposes. Use it to override the standard detection of nodes.

Max length: 256


## <a name="next-steps"></a>Next steps

- Learn how to [extend and filter telemetry](app-insights-api-filtering-sampling.md).
- See [data model](application-insights-data-model.md) for Application Insights types and data model.
- Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).
