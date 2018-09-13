---
title: How to document data sources | Microsoft Docs
description: How-to article highlighting how to document data assets in Azure Data Catalog.
services: data-catalog
documentationcenter: ''
author: spelluru
manager: NA
editor: ''
tags: ''
ms.assetid: 053b1701-b848-4ada-b726-6f485caa9961
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 01/19/2017
ms.author: spelluru
ms.openlocfilehash: e0c490822ebb17387323403e7330394267274ead
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553459"
---
# <a name="document-data-sources"></a><span data-ttu-id="f59f4-103">Document data sources</span><span class="sxs-lookup"><span data-stu-id="f59f4-103">Document data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="f59f4-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="f59f4-104">Introduction</span></span>
<span data-ttu-id="f59f4-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span><span class="sxs-lookup"><span data-stu-id="f59f4-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="f59f4-106">In other words, **Azure Data Catalog** is all about helping people discover, *understand*, and use data sources, and helping organizations to get more value from their existing data.</span><span class="sxs-lookup"><span data-stu-id="f59f4-106">In other words, **Azure Data Catalog** is all about helping people discover, *understand*, and use data sources, and helping organizations to get more value from their existing data.</span></span>

<span data-ttu-id="f59f4-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by the service, but the story doesn’t end there.</span><span class="sxs-lookup"><span data-stu-id="f59f4-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by the service, but the story doesn’t end there.</span></span> <span data-ttu-id="f59f4-108">**Azure Data Catalog** also allows users to provide their own complete documentation that can describe the usage and common scenarios for the data source.</span><span class="sxs-lookup"><span data-stu-id="f59f4-108">**Azure Data Catalog** also allows users to provide their own complete documentation that can describe the usage and common scenarios for the data source.</span></span>

<span data-ttu-id="f59f4-109">In [How to annotate data sources](data-catalog-how-to-annotate.md), you learn that experts who know the data source can annotate it with tags and a description.</span><span class="sxs-lookup"><span data-stu-id="f59f4-109">In [How to annotate data sources](data-catalog-how-to-annotate.md), you learn that experts who know the data source can annotate it with tags and a description.</span></span> <span data-ttu-id="f59f4-110">The **Azure Data Catalog** portal includes a rich text editor so that users can fully document data assets and containers.</span><span class="sxs-lookup"><span data-stu-id="f59f4-110">The **Azure Data Catalog** portal includes a rich text editor so that users can fully document data assets and containers.</span></span> <span data-ttu-id="f59f4-111">The editor includes paragraph formatting, such as headings, text formatting, bulleted lists, numbered lists, and tables.</span><span class="sxs-lookup"><span data-stu-id="f59f4-111">The editor includes paragraph formatting, such as headings, text formatting, bulleted lists, numbered lists, and tables.</span></span>

<span data-ttu-id="f59f4-112">Tags and descriptions are great for simple annotations.</span><span class="sxs-lookup"><span data-stu-id="f59f4-112">Tags and descriptions are great for simple annotations.</span></span> <span data-ttu-id="f59f4-113">However, to help data consumers better understand the use of a data source, and business scenarios for a data source, an expert can provide complete, detailed documentation.</span><span class="sxs-lookup"><span data-stu-id="f59f4-113">However, to help data consumers better understand the use of a data source, and business scenarios for a data source, an expert can provide complete, detailed documentation.</span></span> <span data-ttu-id="f59f4-114">It's easy to document a data source.</span><span class="sxs-lookup"><span data-stu-id="f59f4-114">It's easy to document a data source.</span></span> <span data-ttu-id="f59f4-115">Select a data asset or container, and choose **Documentation**.</span><span class="sxs-lookup"><span data-stu-id="f59f4-115">Select a data asset or container, and choose **Documentation**.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-documentation/data-catalog-documentation.png)

## <a name="documenting-data-assets"></a><span data-ttu-id="f59f4-116">Documenting data assets</span><span class="sxs-lookup"><span data-stu-id="f59f4-116">Documenting data assets</span></span>
<span data-ttu-id="f59f4-117">The benefit of **Azure Data Catalog** documentation allows you to use your Data Catalog as a content repository to create a complete narrative of your data assets.</span><span class="sxs-lookup"><span data-stu-id="f59f4-117">The benefit of **Azure Data Catalog** documentation allows you to use your Data Catalog as a content repository to create a complete narrative of your data assets.</span></span> <span data-ttu-id="f59f4-118">You can explore detailed content that describes containers and tables.</span><span class="sxs-lookup"><span data-stu-id="f59f4-118">You can explore detailed content that describes containers and tables.</span></span> <span data-ttu-id="f59f4-119">If you already have content in another content repository, such as SharePoint or a file share, you can add to the asset documentation links to reference this existing content.</span><span class="sxs-lookup"><span data-stu-id="f59f4-119">If you already have content in another content repository, such as SharePoint or a file share, you can add to the asset documentation links to reference this existing content.</span></span> <span data-ttu-id="f59f4-120">This feature makes your existing documents more discoverable.</span><span class="sxs-lookup"><span data-stu-id="f59f4-120">This feature makes your existing documents more discoverable.</span></span>

> [!NOTE]
> <span data-ttu-id="f59f4-121">Documentation is not included in search index.</span><span class="sxs-lookup"><span data-stu-id="f59f4-121">Documentation is not included in search index.</span></span>
>
>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-documentation/data-catalog-documentation2.png)

<span data-ttu-id="f59f4-122">The level of documentation can range from describing the characteristics and value of a data asset container to a detailed description of table schema within a container.</span><span class="sxs-lookup"><span data-stu-id="f59f4-122">The level of documentation can range from describing the characteristics and value of a data asset container to a detailed description of table schema within a container.</span></span> <span data-ttu-id="f59f4-123">The level of documentation provided should be driven by your business needs.</span><span class="sxs-lookup"><span data-stu-id="f59f4-123">The level of documentation provided should be driven by your business needs.</span></span> <span data-ttu-id="f59f4-124">But in general, here are a few pros and cons of documenting data assets:</span><span class="sxs-lookup"><span data-stu-id="f59f4-124">But in general, here are a few pros and cons of documenting data assets:</span></span>

* <span data-ttu-id="f59f4-125">Document just a container: All the content is in one place, but might lack necessary details for users to make an informed decision.</span><span class="sxs-lookup"><span data-stu-id="f59f4-125">Document just a container: All the content is in one place, but might lack necessary details for users to make an informed decision.</span></span>
* <span data-ttu-id="f59f4-126">Document just the tables: Content is specific to that object, but your users have multiple places for documents.</span><span class="sxs-lookup"><span data-stu-id="f59f4-126">Document just the tables: Content is specific to that object, but your users have multiple places for documents.</span></span>
* <span data-ttu-id="f59f4-127">Document containers and tables: Most comprehensive approach, but might introduce more maintenance of the documents.</span><span class="sxs-lookup"><span data-stu-id="f59f4-127">Document containers and tables: Most comprehensive approach, but might introduce more maintenance of the documents.</span></span>

## <a name="summary"></a><span data-ttu-id="f59f4-128">Summary</span><span class="sxs-lookup"><span data-stu-id="f59f4-128">Summary</span></span>
<span data-ttu-id="f59f4-129">Documenting data sources with **Azure Data Catalog** can create a narrative about your data assets in as much detail as you need.</span><span class="sxs-lookup"><span data-stu-id="f59f4-129">Documenting data sources with **Azure Data Catalog** can create a narrative about your data assets in as much detail as you need.</span></span>  <span data-ttu-id="f59f4-130">By using links, you can link to content stored in an existing content repository, which brings your existing docs and data assets together.</span><span class="sxs-lookup"><span data-stu-id="f59f4-130">By using links, you can link to content stored in an existing content repository, which brings your existing docs and data assets together.</span></span> <span data-ttu-id="f59f4-131">Once your users discover appropriate data assets, they can have a complete set of documentation.</span><span class="sxs-lookup"><span data-stu-id="f59f4-131">Once your users discover appropriate data assets, they can have a complete set of documentation.</span></span>

