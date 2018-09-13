---
title: Azure CLI examples - Azure Media Services | Microsoft Docs
description: Azure CLI examples for Azure Media Services service
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.custom: ''
ms.date: 04/15/2018
ms.author: juliako
ms.openlocfilehash: 3328403f5366f168f979a14951da938f26e1aee9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965792"
---
# <a name="azure-cli-examples-for-azure-media-services"></a><span data-ttu-id="a6aeb-103">Azure CLI examples for Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="a6aeb-103">Azure CLI examples for Azure Media Services</span></span>

<span data-ttu-id="a6aeb-104">The following table includes links to the Azure CLI examples for Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="a6aeb-104">The following table includes links to the Azure CLI examples for Azure Media Services.</span></span>

|  |  |
|---|---|
|<span data-ttu-id="a6aeb-105">**Account**</span><span class="sxs-lookup"><span data-stu-id="a6aeb-105">**Account**</span></span>||
| [<span data-ttu-id="a6aeb-106">Create a Media Services account</span><span class="sxs-lookup"><span data-stu-id="a6aeb-106">Create a Media Services account</span></span>](./scripts/cli-create-account.md) | <span data-ttu-id="a6aeb-107">Creates an Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="a6aeb-107">Creates an Azure Media Services account.</span></span> <span data-ttu-id="a6aeb-108">Also, creates a service principal that can be used to access APIs to programmatically manage the account.</span><span class="sxs-lookup"><span data-stu-id="a6aeb-108">Also, creates a service principal that can be used to access APIs to programmatically manage the account.</span></span> |
| [<span data-ttu-id="a6aeb-109">Reset account credentials</span><span class="sxs-lookup"><span data-stu-id="a6aeb-109">Reset account credentials</span></span>](./scripts/cli-reset-account-credentials.md)|<span data-ttu-id="a6aeb-110">Resets your account credentials and gets the app.config settings back.</span><span class="sxs-lookup"><span data-stu-id="a6aeb-110">Resets your account credentials and gets the app.config settings back.</span></span>|
|<span data-ttu-id="a6aeb-111">**Assets**</span><span class="sxs-lookup"><span data-stu-id="a6aeb-111">**Assets**</span></span>||
| [<span data-ttu-id="a6aeb-112">Create assets</span><span class="sxs-lookup"><span data-stu-id="a6aeb-112">Create assets</span></span>](./scripts/cli-create-asset.md)|<span data-ttu-id="a6aeb-113">Creates a Media Services Asset to upload content to.</span><span class="sxs-lookup"><span data-stu-id="a6aeb-113">Creates a Media Services Asset to upload content to.</span></span>|
| [<span data-ttu-id="a6aeb-114">Upload a file</span><span class="sxs-lookup"><span data-stu-id="a6aeb-114">Upload a file</span></span>](./scripts/cli-upload-file-asset.md)|<span data-ttu-id="a6aeb-115">Uploads a local file to a storage container.</span><span class="sxs-lookup"><span data-stu-id="a6aeb-115">Uploads a local file to a storage container.</span></span>|
| [<span data-ttu-id="a6aeb-116">Publish an asset</span><span class="sxs-lookup"><span data-stu-id="a6aeb-116">Publish an asset</span></span>](./scripts/cli-publish-asset.md)| <span data-ttu-id="a6aeb-117">Creates a  Streaming Locator and gets Streaming URLs back.</span><span class="sxs-lookup"><span data-stu-id="a6aeb-117">Creates a  Streaming Locator and gets Streaming URLs back.</span></span> |
| <span data-ttu-id="a6aeb-118">**Transforms** and **Jobs**</span><span class="sxs-lookup"><span data-stu-id="a6aeb-118">**Transforms** and **Jobs**</span></span>||
| [<span data-ttu-id="a6aeb-119">Create transforms</span><span class="sxs-lookup"><span data-stu-id="a6aeb-119">Create transforms</span></span>](./scripts/cli-create-transform.md)|<span data-ttu-id="a6aeb-120">Shows how to create transforms.</span><span class="sxs-lookup"><span data-stu-id="a6aeb-120">Shows how to create transforms.</span></span> <span data-ttu-id="a6aeb-121">Transforms describe a simple workflow of tasks for processing your video or audio files (often referred to as a "recipe").</span><span class="sxs-lookup"><span data-stu-id="a6aeb-121">Transforms describe a simple workflow of tasks for processing your video or audio files (often referred to as a "recipe").</span></span><br/> <span data-ttu-id="a6aeb-122">You should always check if a Transform with desired name and "recipe" already exist.</span><span class="sxs-lookup"><span data-stu-id="a6aeb-122">You should always check if a Transform with desired name and "recipe" already exist.</span></span> <span data-ttu-id="a6aeb-123">If it does, reuse it.</span><span class="sxs-lookup"><span data-stu-id="a6aeb-123">If it does, reuse it.</span></span> |
| [<span data-ttu-id="a6aeb-124">Create jobs</span><span class="sxs-lookup"><span data-stu-id="a6aeb-124">Create jobs</span></span>](./scripts/cli-create-jobs.md)|<span data-ttu-id="a6aeb-125">Submits a Job to a simple encoding Transform using HTTPs URL.</span><span class="sxs-lookup"><span data-stu-id="a6aeb-125">Submits a Job to a simple encoding Transform using HTTPs URL.</span></span>|
| [<span data-ttu-id="a6aeb-126">Create EventGrid</span><span class="sxs-lookup"><span data-stu-id="a6aeb-126">Create EventGrid</span></span>](./scripts/cli-create-event-grid.md)|<span data-ttu-id="a6aeb-127">Creates an account level Event Grid subscription for Job State Changes.</span><span class="sxs-lookup"><span data-stu-id="a6aeb-127">Creates an account level Event Grid subscription for Job State Changes.</span></span>|

## <a name="see-also"></a><span data-ttu-id="a6aeb-128">See also</span><span class="sxs-lookup"><span data-stu-id="a6aeb-128">See also</span></span>

[<span data-ttu-id="a6aeb-129">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a6aeb-129">Azure CLI</span></span>](https://docs.microsoft.com/en-us/cli/azure/ams?view=azure-cli-latest)
