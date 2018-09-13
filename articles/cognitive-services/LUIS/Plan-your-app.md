---
title: Plan your LUIS applications | Microsoft Docs
description: Outline relevant app intents and entities, and then create your application plans in Language Understanding Intelligent Services (LUIS).
services: cognitive-services
author: cahann
manager: hsalama
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 03/01/2017
ms.author: cahann
ms.openlocfilehash: 10366f34307f9035f921a57a2a8b4cd1cce54a44
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550406"
---
# <a name="plan-your-application"></a><span data-ttu-id="6110a-103">Plan Your Application</span><span class="sxs-lookup"><span data-stu-id="6110a-103">Plan Your Application</span></span>
<span data-ttu-id="6110a-104">All LUIS applications are centered around a domain-specific topic, for example booking of tickets, flights, hotels, rental cars etc. or content related to exercising, tracking fitness efforts and setting goals.</span><span class="sxs-lookup"><span data-stu-id="6110a-104">All LUIS applications are centered around a domain-specific topic, for example booking of tickets, flights, hotels, rental cars etc. or content related to exercising, tracking fitness efforts and setting goals.</span></span> <span data-ttu-id="6110a-105">It is advisable to plan your application before you start creating it in LUIS.</span><span class="sxs-lookup"><span data-stu-id="6110a-105">It is advisable to plan your application before you start creating it in LUIS.</span></span> <span data-ttu-id="6110a-106">Prepare an outline (schema) of the possible intents and entities that are relevant to the domain-specific topic of your application.</span><span class="sxs-lookup"><span data-stu-id="6110a-106">Prepare an outline (schema) of the possible intents and entities that are relevant to the domain-specific topic of your application.</span></span>  

<span data-ttu-id="6110a-107">Let's take the example of a virtual travel booking agency application.</span><span class="sxs-lookup"><span data-stu-id="6110a-107">Let's take the example of a virtual travel booking agency application.</span></span> <span data-ttu-id="6110a-108">You should think about the intents and entities that are important to your application’s task.</span><span class="sxs-lookup"><span data-stu-id="6110a-108">You should think about the intents and entities that are important to your application’s task.</span></span> <span data-ttu-id="6110a-109">In a travel booking application, users would like to book a flight and get an idea of the weather at their travel destination.</span><span class="sxs-lookup"><span data-stu-id="6110a-109">In a travel booking application, users would like to book a flight and get an idea of the weather at their travel destination.</span></span> <span data-ttu-id="6110a-110">Thus, the relevant intents would be "BookFlight" and "GetWeather".</span><span class="sxs-lookup"><span data-stu-id="6110a-110">Thus, the relevant intents would be "BookFlight" and "GetWeather".</span></span> <span data-ttu-id="6110a-111">For flight booking, some relevant information is needed such as the location, date, airline, tickets' category and travel class.</span><span class="sxs-lookup"><span data-stu-id="6110a-111">For flight booking, some relevant information is needed such as the location, date, airline, tickets' category and travel class.</span></span> <span data-ttu-id="6110a-112">Thus, they can be added as entities.</span><span class="sxs-lookup"><span data-stu-id="6110a-112">Thus, they can be added as entities.</span></span> 

<span data-ttu-id="6110a-113">With a planned outline of intents and entities, you can start creating your application in LUIS and define these intents and entities.</span><span class="sxs-lookup"><span data-stu-id="6110a-113">With a planned outline of intents and entities, you can start creating your application in LUIS and define these intents and entities.</span></span>

<span data-ttu-id="6110a-114">[Click here](create-new-app.md) to know how to create a new app.</span><span class="sxs-lookup"><span data-stu-id="6110a-114">[Click here](create-new-app.md) to know how to create a new app.</span></span>
