---
title: Academic Knowledge API for Microsoft Academic Graph | Microsoft Docs
description: Use the Academic Knowledge API to interpret user queries and retrieve rich information from the Academic Graph in Microsoft Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.technology: academic-knowledge
ms.topic: article
ms.date: 03/27/2017
ms.author: alch
ms.openlocfilehash: b27e3a6352a3d9cd9d77ab1802517fd6b9268bf8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671109"
---
# <a name="academic-knowledge-api"></a>Academic Knowledge API

Welcome to the Academic Knowledge API. With this service, you will be able to interpret user queries for academic intent and retrieve rich information from the Microsoft Academic Graph (MAG). The MAG knowledge base is a web-scale heterogeneous entity graph comprised of entities that model scholarly activities: field of study, author, institution, paper, venue, and event. 

The MAG data is mined from the Bing web index as well as an in-house knowledge base from Bing. As a result of on-going Bing indexing, this API will contain fresh information from the Web following discovery and indexing by Bing. Based on this dataset, the Academic Knowledge APIs enables a knowledge-driven, interactive dialog that seamlessly combines reactive search with proactive suggestion experiences, rich research paper graph search results, and histogram distributions of the attribute values for a set of papers and related entities.

For more information on the Microsoft Academic Graph, see [http://aka.ms/academicgraph](http://aka.ms/academicgraph).

## <a name="features"></a>Features
The Academic Knowledge API consists of four related REST endpoints:  
  1. **interpret** – Interprets a natural language user query string. Returns annotated interpretations to enable rich search-box auto-completion experiences that anticipate what the user is typing.  
  2. **evaluate** – Evaluates a query expression and returns Academic Knowledge entity results.  
  3. **calchistogram** – Calculates a histogram of the distribution of attribute values for the academic entities returned by a query expression, such as the distribution of citations by year for a given author.  
  4. **graph search** – Searches for a given graph pattern and returns the matched entity results.

Used together, these API methods allow you to create a rich semantic search experience. Given a user query string, the **interpret** method provides you with an annotated version of the query and a structured query expression, while optionally completing the user’s query based on the semantics of the underlying academic data. For example, if a user types the string *latent s*, the **interpret** method can provide a set of ranked interpretations, suggesting that the user might be searching for the field of study *latent semantic analysis*, the paper *latent structure analysis*, or other entity expressions starting with *latent s*. This information can be used to quickly guide the user to the desired search results.

The **evaluate** method can be used to retrieve a set of matching paper entities from the academic knowledge base, and the **calchistogram** method can be used to calculate the distribution of attribute values for a set of paper entities which can be used to further filter the search results.        

The **graph search** method has two modes: *json* and *lambda*. The *json* mode can perform graph pattern matching according to the graph patterns specified by a JSON object. The *lambda* mode can perform server-side computations during graph traversals according to the user-specified lambda expressions.

## <a name="getting-started"></a>Getting Started 
Please see the subtopics at the left for detailed documentation.  Note that to improve the readability of the examples, the REST API calls contain characters (such as spaces) that have not been URL-encoded.  Your code will need to apply the appropriate URL-encodings.
