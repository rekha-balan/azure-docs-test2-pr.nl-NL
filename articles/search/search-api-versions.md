---
title: API versions of Azure Search | Microsoft Docs
description: Version policy for Azure Search REST APIs and the client library in the .NET SDK.
author: brjohnstmsft
manager: jlembicz
services: search
ms.service: search
ms.devlang: dotnet
ms.topic: conceptual
ms.date: 06/28/2018
ms.author: brjohnst
ms.openlocfilehash: 8d1e30b0bca3c63fe4528c06e5389d8cbe27a7e6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44818368"
---
# <a name="api-versions-in-azure-search"></a>API versions in Azure Search
Azure Search rolls out feature updates regularly. Sometimes, but not always, these updates require a new version of the API to preserve backward compatibility. Publishing a new version allows you to control when and how you integrate search service updates in your code.

As a rule, the Azure Search team publishes new versions only when necessary, since it can involve some effort to upgrade your code to use a new API version. A new version is needed only if some aspect of the API has changed in a way that breaks backward compatibility. Such changes can happen because of fixes to existing features, or because of new features that change existing API surface area.

The same rule applies for SDK updates. The Azure Search SDK follows the [semantic versioning](http://semver.org/) rules, which means that its version has three parts: major, minor, and build number (for example, 1.1.0). A new major version of the SDK is released only for changes that break backward compatibility. Non-breaking feature updates will increment the minor version, and bug fixes will only increase the build version.

> [!NOTE]
> Your Azure Search service instance supports several REST API versions, including the latest one. You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version. When using the REST API, you must specify the API version in every request via the api-version parameter. When using the .NET SDK, the version of the SDK you’re using determines the corresponding version of the REST API. If you are using an older SDK, you can continue to run that code with no changes even if the service is upgraded to support a newer API version.

## <a name="snapshot-of-current-versions"></a>Snapshot of current versions
Below is a snapshot of the current versions of all programming interfaces to Azure Search.

| Interfaces | Most recent major version | Status |
| --- | --- | --- |
| [.NET SDK](https://aka.ms/search-sdk) |5.0 |Generally Available, released April 2018 |
| [.NET SDK Preview](https://aka.ms/search-sdk-preview) |4.0.1-preview |Preview, released May 2017 |
| [Service REST API](https://docs.microsoft.com/rest/api/searchservice/) |2017-11-11 |Generally Available |
| [Service REST API 2017-11-11-Preview](search-api-2017-11-11-preview.md) |2017-11-11-Preview |Preview |
| [.NET Management SDK](https://aka.ms/search-mgmt-sdk) |2.0 |Generally Available |
| [Management REST API](https://docs.microsoft.com/rest/api/searchmanagement/) |2015-08-19 |Generally Available |

For the REST APIs, including the `api-version` on each call is required. Using `api-version` makes it easy to target a specific version, such as a preview API. The following example illustrates how the `api-version` parameter is specified:

    GET https://adventure-works.search.windows.net/indexes/bikes?api-version=2017-11-11

> [!NOTE]
> Although each request has an `api-version`, we recommend that you use the same version for all API requests. This is especially true when new API versions introduce attributes or operations that are not recognized by previous versions. Mixing API versions can have unintended consequences and should be avoided.
>
> The Service REST API and Management REST API are versioned independently of each other. Any similarity in version numbers is coincidental.

Generally available (or GA) APIs can be used in production and are subject to Azure service level agreements. Preview versions have experimental features that are not always migrated to a GA version. **You are strongly advised to avoid using preview APIs in production applications.**

## <a name="about-preview-and-generally-available-versions"></a>About Preview and Generally Available versions
Azure Search always pre-releases experimental features through the REST API first, then through prerelease versions of the .NET SDK.

Preview features are available for testing and experimentation, with the goal of gathering feedback on feature design and implementation. For this reason, preview features can change over time, possibly in ways that break backwards compatibility. This is in contrast to features in a GA version, which are stable and unlikely to change with the exception of small backward-compatible fixes and enhancements. Also, preview features do not always make it into a GA release.

For these reasons, we recommend against writing production code that takes a dependency on preview versions. If you're using an older preview version, we recommend migrating to the generally available (GA) version.

For the .NET SDK: Guidance for code migration can be found at [Upgrade the .NET SDK](search-dotnet-sdk-migration.md).

General availability means that Azure Search is now under the service level agreement (SLA). The SLA can be found at [Azure Search Service Level Agreements](https://azure.microsoft.com/support/legal/sla/search/v1_0/).
