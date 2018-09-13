---
title: Entity Search SDK Python quickstart | Microsoft Docs
description: Setup for Entity search SDK console application.
titleSuffix: Azure Entity Search SDK Python quickstart
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-entity-search
ms.topic: article
ms.date: 02/15/2018
ms.author: v-gedod
ms.openlocfilehash: 95449fa3753291269e1a83d1431df3bf0cbe372f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856911"
---
# <a name="entity-search-sdk-python-quickstart"></a><span data-ttu-id="60902-103">Entity Search SDK Python quickstart</span><span class="sxs-lookup"><span data-stu-id="60902-103">Entity Search SDK Python quickstart</span></span>

<span data-ttu-id="60902-104">The Entity Search SDK contains the functionality of the REST API for web queries and parsing results.</span><span class="sxs-lookup"><span data-stu-id="60902-104">The Entity Search SDK contains the functionality of the REST API for web queries and parsing results.</span></span>

<span data-ttu-id="60902-105">The [source code for Python Bing Entity Search SDK samples](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples/blob/master/samples/search/entity_search_samples.py) is available on Git Hub.</span><span class="sxs-lookup"><span data-stu-id="60902-105">The [source code for Python Bing Entity Search SDK samples](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples/blob/master/samples/search/entity_search_samples.py) is available on Git Hub.</span></span>

## <a name="application-dependencies"></a><span data-ttu-id="60902-106">Application dependencies</span><span class="sxs-lookup"><span data-stu-id="60902-106">Application dependencies</span></span>
<span data-ttu-id="60902-107">If you don't already have it, install Python.</span><span class="sxs-lookup"><span data-stu-id="60902-107">If you don't already have it, install Python.</span></span> <span data-ttu-id="60902-108">The SDK is compatible with Python 2.7, 3.3, 3.4, 3.5, and 3.6.</span><span class="sxs-lookup"><span data-stu-id="60902-108">The SDK is compatible with Python 2.7, 3.3, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="60902-109">The general recommendation for Python development is to use a [virtual environment](https://docs.python.org/3/tutorial/venv.html).</span><span class="sxs-lookup"><span data-stu-id="60902-109">The general recommendation for Python development is to use a [virtual environment](https://docs.python.org/3/tutorial/venv.html).</span></span> <span data-ttu-id="60902-110">Install and initialize the virtual environment with the [venv module](https://pypi.python.org/pypi/virtualenv).</span><span class="sxs-lookup"><span data-stu-id="60902-110">Install and initialize the virtual environment with the [venv module](https://pypi.python.org/pypi/virtualenv).</span></span> <span data-ttu-id="60902-111">You must install virtualenv for Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="60902-111">You must install virtualenv for Python 2.7.</span></span>
```
python -m venv mytestenv
```
<span data-ttu-id="60902-112">Install Bing Entity Search SDK dependencies:</span><span class="sxs-lookup"><span data-stu-id="60902-112">Install Bing Entity Search SDK dependencies:</span></span>
```
cd mytestenv
python -m pip install azure-cognitiveservices-search-entitysearch
```
## <a name="entity-search-client"></a><span data-ttu-id="60902-113">Entity Search client</span><span class="sxs-lookup"><span data-stu-id="60902-113">Entity Search client</span></span>
<span data-ttu-id="60902-114">Get a [Cognitive Services access key](https://azure.microsoft.com/try/cognitive-services/) under *Search*.</span><span class="sxs-lookup"><span data-stu-id="60902-114">Get a [Cognitive Services access key](https://azure.microsoft.com/try/cognitive-services/) under *Search*.</span></span> <span data-ttu-id="60902-115">Add imports:</span><span class="sxs-lookup"><span data-stu-id="60902-115">Add imports:</span></span>
```
from azure.cognitiveservices.search.entitysearch import EntitySearchAPI
from azure.cognitiveservices.search.entitysearch.models import Place, ErrorResponseException
from msrest.authentication import CognitiveServicesCredentials

subscription_key = "YOUR-SUBSCRIPTION-KEY"
```
<span data-ttu-id="60902-116">Create an instance of the `CognitiveServicesCredentials`.</span><span class="sxs-lookup"><span data-stu-id="60902-116">Create an instance of the `CognitiveServicesCredentials`.</span></span> <span data-ttu-id="60902-117">Instantiate the client:</span><span class="sxs-lookup"><span data-stu-id="60902-117">Instantiate the client:</span></span>
```
client = EntitySearchAPI(CognitiveServicesCredentials(subscription_key))
```
<span data-ttu-id="60902-118">Search for a single entity (Gibralter) and print out a short description:</span><span class="sxs-lookup"><span data-stu-id="60902-118">Search for a single entity (Gibralter) and print out a short description:</span></span>
```
entity_data = client.entities.search(query="Gibralter")

if entity_data.entities.value:
    # find the entity that represents the dominant one

    main_entities = [entity for entity in entity_data.entities.value
                     if entity.entity_presentation_info.entity_scenario == "DominantEntity"]

    if main_entities:
        print('Searched for "Gibralter" and found a dominant entity with this description:')
        print(main_entities[0].description)
    else:
        print("Couldn't find main entity Gibralter!")

else:
    print("Didn't see any data..")

```
<span data-ttu-id="60902-119">Search and handle disambiguation results for an ambiguous query (William Gates).</span><span class="sxs-lookup"><span data-stu-id="60902-119">Search and handle disambiguation results for an ambiguous query (William Gates).</span></span>
```
def handling_disambiguation(subscription_key):

    client = EntitySearchAPI(CognitiveServicesCredentials(subscription_key))

    try:
        entity_data = client.entities.search(query="william gates")

        if entity_data.entities.value:
            # find the entity that represents the dominant one

            main_entities = [entity for entity in entity_data.entities.value
                             if entity.entity_presentation_info.entity_scenario == "DominantEntity"]

            disambig_entities = [entity for entity in entity_data.entities.value
                                 if entity.entity_presentation_info.entity_scenario == "DisambiguationItem"]

            if main_entities:
                main_entity = main_entities[0]
                type_hint = main_entity.entity_presentation_info.entity_type_display_hint
                
                print('Searched for "William Gates" and found a dominant entity {}with this description:'.format(
                    '"with type hint "{}" '.format(type_hint) if type_hint else ''))
                print(main_entity.description)
            else:
                print("Couldn't find a reliable dominant entity for William Gates!")
        
            if disambig_entities:
                print("\nThis query is pretty ambiguous and can be referring to multiple things. Did you mean one of these:")
                suggestions = []
                for disambig_entity in disambig_entities:
                    suggestions.append("{} the {}".format(disambig_entity.name, disambig_entity.entity_presentation_info.entity_type_display_hint))
                print(", or ".join(suggestions))
            else:
                print("We didn't find any disambiguation items for William Gates, so we must be certain what you're talking about!")

        else:
            print("Didn't see any data..")

    except Exception as err:
        print("Encountered exception. {}".format(err))

```
<span data-ttu-id="60902-120">Search for a single store (Microsoft Store) and print out its phone number.</span><span class="sxs-lookup"><span data-stu-id="60902-120">Search for a single store (Microsoft Store) and print out its phone number.</span></span>
```
def store_lookup(subscription_key):

    client = EntitySearchAPI(CognitiveServicesCredentials(subscription_key))

    try:
        entity_data = client.entities.search(query="microsoft store")

        if entity_data.places.value:

            store = entity_data.places.value[0]

            # Some local entities will be places, others won't be. Depending on what class contains the data you want, you can check 
            # using isinstance one of the class, or try to get the attribute and handle the exception (EAFP principle).
            # The recommended Python way is usually EAFP (see https://docs.python.org/3/glossary.html)
            # In this case, the item being returned is technically a store, but the Place schema has the data we want (telephone)

            # Pythonic approach : EAFP "Easier to ask for forgiveness than permission"
            try:
                telephone = store.telephone
                print('Searched for "Microsoft Store" and found a store with this phone number:')
                print(telephone)
            except AttributeError:
                print("Couldn't find a place!")

            # More cross language approach
            if isinstance(store, Place):
                print('Searched for "Microsoft Store" and found a store with this phone number:')
                print(store.telephone)
            else:
                print("Couldn't find a place!")


        else:
            print("Didn't see any data..")

    except Exception as err:
        print("Encountered exception. {}".format(err))

```
<span data-ttu-id="60902-121">Search for a list of restaurants (Seattle restaurants) and print their names and phone numbers.</span><span class="sxs-lookup"><span data-stu-id="60902-121">Search for a list of restaurants (Seattle restaurants) and print their names and phone numbers.</span></span>
```
def multiple_restaurant_lookup(subscription_key):

    client = EntitySearchAPI(CognitiveServicesCredentials(subscription_key))

    try:
        restaurants = client.entities.search(query="seattle restaurants")

        if restaurants.places.value:

            # get all the list items that relate to this query
            list_items = [entity for entity in restaurants.places.value
                          if entity.entity_presentation_info.entity_scenario == "ListItem"]

            if list_items:

                suggestions = []
                for place in list_items:
                    # Pythonic approach : EAFP "Easier to ask for forgiveness than permission"
                    # see https://docs.python.org/3/glossary.html
                    try:
                        suggestions.append("{} ({})".format(place.name, place.telephone))
                    except AttributeError:
                        print("Unexpectedly found something that isn\'t a place named '{}'", place.name)

                print("Ok, we found these places: ")
                print(", ".join(suggestions))

            else:
                print("Couldn't find any relevant results for \"seattle restaurants\"")

        else:
            print("Didn't see any data..")

    except Exception as err:
        print("Encountered exception. {}".format(err))

```
<span data-ttu-id="60902-122">Trigger a bad request and read the error response.</span><span class="sxs-lookup"><span data-stu-id="60902-122">Trigger a bad request and read the error response.</span></span>
```
def error(subscription_key):

    client = EntitySearchAPI(CognitiveServicesCredentials(subscription_key))

    try:
        entity_data = client.entities.search(query="satya nadella", market="no-ty")
    except ErrorResponseException as err:
        # The status code of the error should be a good indication of what occurred. However, if you'd like more details, you can dig into the response.
        # Please note that depending on the type of error, the response schema might be different, so you aren't guaranteed a specific error response schema.
                    
        print("Exception occurred, status code {} with reason {}.\n".format(err.response.status_code, err))

        # if you'd like more descriptive information (if available)
        if err.error.errors:
            print("This is the errors I have:")
            for error in err.error.errors:
                print("Parameter \"{}\" has an invalid value \"{}\". SubCode is \"{}\". Detailed message is \"{}\"".format(error.parameter, error.value, error.sub_code, error.message))
        else:
            print("There was no details on the error.")
```
## <a name="next-steps"></a><span data-ttu-id="60902-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="60902-123">Next steps</span></span>

[<span data-ttu-id="60902-124">Cognitive Services Python SDK samples</span><span class="sxs-lookup"><span data-stu-id="60902-124">Cognitive Services Python SDK samples</span></span>](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples)
