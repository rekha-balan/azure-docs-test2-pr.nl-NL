---
title: Create an Android app on Azure App Service Mobile Apps | Microsoft Docs
description: Follow this tutorial to get started with using Azure mobile app backends for Android development
services: app-service\mobile
documentationcenter: android
author: ysxu
manager: adrianha
editor: ''
ms.assetid: 355f0959-aa7f-472c-a6c7-9eecea3a34a9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: 7752cd091d7952a905001f14414eba84b90f0d51
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554980"
---
# <a name="create-an-android-app"></a><span data-ttu-id="c1b51-103">Create an Android app</span><span class="sxs-lookup"><span data-stu-id="c1b51-103">Create an Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="c1b51-104">Overview</span><span class="sxs-lookup"><span data-stu-id="c1b51-104">Overview</span></span>
<span data-ttu-id="c1b51-105">This tutorial shows you how to add a cloud-based backend service to an Android mobile app by using an Azure mobile app backend.</span><span class="sxs-lookup"><span data-stu-id="c1b51-105">This tutorial shows you how to add a cloud-based backend service to an Android mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="c1b51-106">You will create both a new mobile app backend and a simple *Todo list* Android app that stores app data in Azure.</span><span class="sxs-lookup"><span data-stu-id="c1b51-106">You will create both a new mobile app backend and a simple *Todo list* Android app that stores app data in Azure.</span></span>

<span data-ttu-id="c1b51-107">Completing this tutorial is a prerequisite for all other Android tutorials about using the Mobile Apps feature in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="c1b51-107">Completing this tutorial is a prerequisite for all other Android tutorials about using the Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1b51-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c1b51-108">Prerequisites</span></span>
<span data-ttu-id="c1b51-109">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="c1b51-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="c1b51-110">[Android Developer Tools](https://developer.android.com/sdk/index.html), which includes the Android Studio integrated development environment, and the latest Android platform.</span><span class="sxs-lookup"><span data-stu-id="c1b51-110">[Android Developer Tools](https://developer.android.com/sdk/index.html), which includes the Android Studio integrated development environment, and the latest Android platform.</span></span>
* <span data-ttu-id="c1b51-111">Azure Mobile Android SDK, which is automatically referenced as part of the quickstart project you download.</span><span class="sxs-lookup"><span data-stu-id="c1b51-111">Azure Mobile Android SDK, which is automatically referenced as part of the quickstart project you download.</span></span>
* <span data-ttu-id="c1b51-112">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c1b51-112">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="c1b51-113">Create a new Azure mobile app backend</span><span class="sxs-lookup"><span data-stu-id="c1b51-113">Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-the-server-project"></a><span data-ttu-id="c1b51-114">Configure the server project</span><span class="sxs-lookup"><span data-stu-id="c1b51-114">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-android-app"></a><span data-ttu-id="c1b51-115">Download and run the Android app</span><span class="sxs-lookup"><span data-stu-id="c1b51-115">Download and run the Android app</span></span>
[!INCLUDE [app-service-mobile-android-run-app](../../includes/app-service-mobile-android-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
