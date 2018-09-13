---
title: Data format in the Knowledge Exploration Service API | Microsoft Docs
description: Learn about the data format in the Knowledge Exploration Service (KES) API in Cognitive Services.
services: cognitive-services
author: bojunehsu
manager: stesp
ms.service: cognitive-services
ms.technology: kes
ms.topic: article
ms.date: 03/26/2016
ms.author: paulhsu
ms.openlocfilehash: 85403f693d845abdf3ecd252b73273fd4a1d2c92
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661298"
---
# <a name="data-format"></a><span data-ttu-id="6f32a-103">Data Format</span><span class="sxs-lookup"><span data-stu-id="6f32a-103">Data Format</span></span>
<span data-ttu-id="6f32a-104">The data file describes the list of objects to index.</span><span class="sxs-lookup"><span data-stu-id="6f32a-104">The data file describes the list of objects to index.</span></span>
<span data-ttu-id="6f32a-105">Each line in the file specifies the attribute values of an object in [JSON format](http://json.org/) with UTF-8 encoding.</span><span class="sxs-lookup"><span data-stu-id="6f32a-105">Each line in the file specifies the attribute values of an object in [JSON format](http://json.org/) with UTF-8 encoding.</span></span>
<span data-ttu-id="6f32a-106">In addition to the attributes defined in the [schema](SchemaFormat.md), each object has an optional "logprob" attribute that specifies the relative log probability among the objects.</span><span class="sxs-lookup"><span data-stu-id="6f32a-106">In addition to the attributes defined in the [schema](SchemaFormat.md), each object has an optional "logprob" attribute that specifies the relative log probability among the objects.</span></span>
<span data-ttu-id="6f32a-107">When the service returns objects in order of decreasing probability, we can use "logprob" to indicate the return order of matching objects.</span><span class="sxs-lookup"><span data-stu-id="6f32a-107">When the service returns objects in order of decreasing probability, we can use "logprob" to indicate the return order of matching objects.</span></span>
<span data-ttu-id="6f32a-108">Given a probability *p* between 0 and 1, the corresponding log probability can be computed as log(*p*), where log() is the natural log function.</span><span class="sxs-lookup"><span data-stu-id="6f32a-108">Given a probability *p* between 0 and 1, the corresponding log probability can be computed as log(*p*), where log() is the natural log function.</span></span>
<span data-ttu-id="6f32a-109">When no value is specified for logprob, the default value 0 is used.</span><span class="sxs-lookup"><span data-stu-id="6f32a-109">When no value is specified for logprob, the default value 0 is used.</span></span>

```json
{"logprob":-5.3, "Title":"latent dirichlet allocation", "Year":2003, "Author":{"Name":"david m blei", "Affiliation":"uc berkeley"}, "Author":{"Name":"andrew y ng", "Affiliation":"stanford"}, "Author":{"Name":"michael i jordan", "Affiliation":"uc berkeley"}}
{"logprob":-6.1, "Title":"probabilistic latent semantic indexing", "Year":1999, "Author":{"Name":"thomas hofmann", "Affiliation":"uc berkeley"}}
...
```

<span data-ttu-id="6f32a-110">For String, GUID, and Blob attributes, the value is represented as a quoted JSON string.</span><span class="sxs-lookup"><span data-stu-id="6f32a-110">For String, GUID, and Blob attributes, the value is represented as a quoted JSON string.</span></span>  <span data-ttu-id="6f32a-111">For numeric attributes (Int32, Int64, Double), the value is represented as a JSON number.</span><span class="sxs-lookup"><span data-stu-id="6f32a-111">For numeric attributes (Int32, Int64, Double), the value is represented as a JSON number.</span></span>  <span data-ttu-id="6f32a-112">For composite attributes, the value is a JSON object that specifies the sub-attribute values.</span><span class="sxs-lookup"><span data-stu-id="6f32a-112">For composite attributes, the value is a JSON object that specifies the sub-attribute values.</span></span>  <span data-ttu-id="6f32a-113">For faster index builds, presort the objects by decreasing log probability.</span><span class="sxs-lookup"><span data-stu-id="6f32a-113">For faster index builds, presort the objects by decreasing log probability.</span></span>

<span data-ttu-id="6f32a-114">In general, an attribute may have 0 or more values.</span><span class="sxs-lookup"><span data-stu-id="6f32a-114">In general, an attribute may have 0 or more values.</span></span>  <span data-ttu-id="6f32a-115">If an attribute has no value, we simply drop it from the JSON.</span><span class="sxs-lookup"><span data-stu-id="6f32a-115">If an attribute has no value, we simply drop it from the JSON.</span></span>  <span data-ttu-id="6f32a-116">If an attribute has 2 or more values, we can repeat the attribute value pair in the JSON object.</span><span class="sxs-lookup"><span data-stu-id="6f32a-116">If an attribute has 2 or more values, we can repeat the attribute value pair in the JSON object.</span></span>  <span data-ttu-id="6f32a-117">Alternatively, we can assign a JSON array containing the multiple values to the attribute.</span><span class="sxs-lookup"><span data-stu-id="6f32a-117">Alternatively, we can assign a JSON array containing the multiple values to the attribute.</span></span>

```json
{"logprob":0, "Title":"0 keyword"}
{"logprob":0, "Title":"1 keyword", "Keyword":"foo"}
{"logprob":0, "Title":"2 keywords", "Keyword":"foo", "Keyword":"bar"}
{"logprob":0, "Title":"2 keywords (alt)", "Keyword":["foo", "bar"]}
```
