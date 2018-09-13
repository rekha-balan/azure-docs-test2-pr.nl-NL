---
title: Azure AD v2 Windows Desktop Getting Started - Config | Microsoft Docs
description: How a Windows Desktop .NET (XAML) application can get an access token and call an API protected by Azure Active Directory v2 endpoint.
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mtillman
editor: ''
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: c42f40252733f0c4fd7fdbabb49714ea537acc70
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866624"
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="9d211-103">Add the application’s registration information to your app</span><span class="sxs-lookup"><span data-stu-id="9d211-103">Add the application’s registration information to your app</span></span>
<span data-ttu-id="9d211-104">In this step, you need to add the Application Id to your project.</span><span class="sxs-lookup"><span data-stu-id="9d211-104">In this step, you need to add the Application Id to your project.</span></span>

1.  <span data-ttu-id="9d211-105">Open `App.xaml.cs` and replace the line containing the `ClientId` with:</span><span class="sxs-lookup"><span data-stu-id="9d211-105">Open `App.xaml.cs` and replace the line containing the `ClientId` with:</span></span>

```csharp
private static string ClientId = "[Enter the application Id here]";
```

### <a name="what-is-next"></a><span data-ttu-id="9d211-106">What is Next</span><span class="sxs-lookup"><span data-stu-id="9d211-106">What is Next</span></span>

[!INCLUDE [Test and Validate](..\..\..\..\includes\active-directory-develop-guidedsetup-windesktop-test.md)]
