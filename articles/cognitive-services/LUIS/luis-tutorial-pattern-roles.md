---
title: Tutorial using pattern roles to improve LUIS predictions - Azure | Microsoft Docs
titleSuffix: Cognitive Services
description: In this tutorial, use pattern roles for contextually related entities to improve LUIS predictions.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 08/03/2018
ms.author: diberry
ms.openlocfilehash: 6f3e7c9db7bbdb6bc24d123208355fc7a1d8e7e8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869033"
---
# <a name="tutorial-improve-app-with-pattern-roles"></a>Tutorial: Improve app with pattern roles

In this tutorial, use a simple entity with roles combined with patterns to increase intent and entity prediction.  When using patterns, fewer example utterances are needed for the intent.

> [!div class="checklist"]
* Understand pattern roles
* Use simple entity with roles 
* Create pattern for utterances using simple entity with roles
* How to verify pattern prediction improvements

[!INCLUDE [LUIS Free account](../../../includes/cognitive-services-luis-free-key-short.md)]

## <a name="before-you-begin"></a>Before you begin
If you don't have the Human Resources app from the [pattern](luis-tutorial-pattern.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website. The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-patterns-HumanResources-v2.json) GitHub repository.

If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `roles`. Cloning is a great way to play with various LUIS features without affecting the original version. 

## <a name="the-purpose-of-roles"></a>The purpose of roles
The purpose of roles is to extract contextually-related entities in an utterance. In the utterance, `Move new employee Robert Williams from Sacramento and San Francisco`, the origin city, and destination city values are related to each other and use common language to denote each location. 

When using patterns, any entities in the pattern must be detected _before_ the pattern matches the utterance. 

When you create a pattern, the first step is to select the intent for the pattern. By selecting the intent, if the pattern matches, the correct intent is always returned with a high score ( usually 99-100%). 

### <a name="compare-hierarchical-entity-to-simple-entity-with-roles"></a>Compare hierarchical entity to simple entity with roles

In the [hierarchical tutorial](luis-quickstart-intent-and-hier-entity.md), the **MoveEmployee** intent detected when to move an existing employee from one building and office to another. The example utterances had origin and destination locations but did not use roles. Instead, the origin and destination were children of the  hierarchical entity. 

In this tutorial, the Human Resources app detects utterances about moving new employees from one city to another. These two types of utterances are similar but solved with different LUIS abilities.

|Tutorial|Example utterance|Origin and destination locations|
|--|--|--|
|[Hierarchical (no roles)](luis-quickstart-intent-and-hier-entity.md)|mv Jill Jones from **a-2349** to **b-1298**|a-2349, b-1298|
|This tutorial (with roles)|Move Billy Patterson from **Yuma** to **Denver**.|Yuma, Denver|

You can't use the hierarchical entity in the pattern because only hierarchical parents are used in patterns. In order to return the named locations of origin and destination, you muse use a pattern.

### <a name="simple-entity-for-new-employee-name"></a>Simple entity for new employee name
The name of the new employee, Billy Patterson, is not part of the list entity **Employee** yet. The new employee name is extracted first, in order to send the name to an external system to create the company credentials. After the company credentials are created, the employee credentials are added to the list entity **Employee**.

The **Employee** list was created in the [list tutorial](luis-quickstart-intent-and-list-entity.md).

The **NewEmployee** entity is a simple entity with no roles. 

### <a name="simple-entity-with-roles-for-relocation-cities"></a>Simple entity with roles for relocation cities
The new employee and family need to be moved from the current city to a city where the fictitious company is located. Because a new employee can come from any city, the locations need to be discovered. A set list such as a list entity would not work because only the cities in the list would be extracted.

The role names associated with the origin and destination cities need to be unique across all entities. An easy way to make sure the roles are unique is to tie them to the containing entity through a naming strategy. The **NewEmployeeRelocation** entity is a simple entity with two roles: **NewEmployeeReloOrigin** and **NewEmployeeReloDestination**.

### <a name="simple-entities-need-enough-examples-to-be-detected"></a>Simple entities need enough examples to be detected
Because the example utterance `Move new employee Robert Williams from Sacramento and San Francisco` has only machine-learned entities, it is important to provide enough example utterances to the intent so the entities are detected.  

**While patterns allow you to provide fewer example utterances, if the entities are not detected, the pattern does not match.**

If you have difficulty with simple entity detection because it is a name such as a city, consider adding a phrase list of similar values. This helps the detection of the city name by giving LUIS an additional signal about that type of word or phrase. Phrase lists only help the pattern by helping with entity detection, which is necessary for the pattern to match. 

## <a name="create-new-entities"></a>Create new entities
1. Select **Build** in the top menu.

2. Select **Entities** from the left navigation. 

3. Select **Create new entity**.

4. In the pop-up window, enter `NewEmployee` as a **Simple** entity.

5. Select **Create new entity**.

6. In the pop-up window, enter `NewEmployeeRelocation` as a **Simple** entity.

7. Select **NewEmployeeRelocation** from the list of entities. 

8. Enter the first role as `NewEmployeeReloOrigin` and select enter.

9. Enter the second role as `NewEmployeeReloDestination` and select enter.

## <a name="create-new-intent"></a>Create new intent
Labeling the entities in these steps may be easier if the prebuilt keyPhrase entity is removed before beginning then added back after you are done with the steps in this section. 

1. Select **Intents** from the left navigation.

2. Select **Create new intent**. 

3. Enter `NewEmployeeRelocationProcess` as the intent name in the pop-up dialog box.

4. Enter the following example utterances, labeling the new entities. The entity and role values are in bold. Remember to switch to the **Tokens View** if you find it easier to label the text. 

    You don't specify the role of the entity when labeling in the intent. You do that later when creating the pattern. 

    |Utterance|NewEmployee|NewEmployeeRelocation|
    |--|--|--|
    |Move **Bob Jones** from **Seattle** to **Los Colinas**|Bob Jones|Seattle, Los Colinas|
    |Move **Dave C. Cooper** from **Redmond** to **New York City**|Dave C. Cooper|Redmond, New York City|
    |Move **Jim Paul Smith** from **Toronto** to **West Vancouver**|Jim Paul Smith|Toronto, West Vancouver|
    |Move **J. Benson** from **Boston** to **Staines-upon-Thames**|J. Benson|Boston, Staines-upon-Thames|
    |Move **Travis "Trav" Hinton** from **Castelo Branco** to **Orlando**|Travis "Trav" Hinton|Castelo Branco, Orlando|
    |Move **Trevor Nottington III** from **Aranda de Duero** to **Boise**|Trevor Nottington III|Aranda de Duero, Boise|
    |Move **Dr. Greg Williams** from **Orlando** to **Ellicott City**|Dr. Greg Williams|Orlando, Ellicott City|
    |Move **Robert "Bobby" Gregson** from **Kansas City** to **San Juan Capistrano**|Robert "Bobby" Gregson|Kansas City, San Juan Capistrano|
    |Move **Patti Owens** from **Bellevue** to **Rockford**|Patti Owens|Bellevue, Rockford|
    |Move **Janet Bartlet** from **Tuscan** to **Santa Fe**|Janet Bartlet|Tuscan, Santa Fe|

    The employee name has a variety of prefix, word count, syntax, and suffix. This is important for LUIS to understand the variations of a new employee name. The city names also have a variety of word count and syntax. This variety is important to teach LUIS how these entities may appear in a user's utterance. 
    
    If either entity had been of the same word count and no other variations, you would teach LUIS that this entity only has that word count and no other variations. LUIS would not be able to correctly predict a broader set of variations because it was not shown any. 

    If you removed the keyPhrase entity, add it back to the app now.

## <a name="train-the-luis-app"></a>Train the LUIS app

[!INCLUDE [LUIS How to Train steps](../../../includes/cognitive-services-luis-tutorial-how-to-train.md)]

## <a name="publish-the-app-to-get-the-endpoint-url"></a>Publish the app to get the endpoint URL

[!INCLUDE [LUIS How to Publish steps](../../../includes/cognitive-services-luis-tutorial-how-to-publish.md)]

## <a name="query-the-endpoint-without-pattern"></a>Query the endpoint without pattern

1. [!INCLUDE [LUIS How to get endpoint first step](../../../includes/cognitive-services-luis-tutorial-how-to-get-endpoint.md)] 

2. Go to the end of the URL in the address and enter `Move Wayne Berry from Miami to Mount Vernon`. The last querystring parameter is `q`, the utterance **query**. 

    ```JSON
    {
      "query": "Move Wayne Berry from Newark to Columbus",
      "topScoringIntent": {
        "intent": "NewEmployeeRelocationProcess",
        "score": 0.514479756
      },
      "intents": [
        {
          "intent": "NewEmployeeRelocationProcess",
          "score": 0.514479756
        },
        {
          "intent": "Utilities.Confirm",
          "score": 0.017118983
        },
        {
          "intent": "MoveEmployee",
          "score": 0.009982505
        },
        {
          "intent": "GetJobInformation",
          "score": 0.008637771
        },
        {
          "intent": "ApplyForJob",
          "score": 0.007115978
        },
        {
          "intent": "Utilities.StartOver",
          "score": 0.006120186
        },
        {
          "intent": "Utilities.Cancel",
          "score": 0.00452428637
        },
        {
          "intent": "None",
          "score": 0.00400899537
        },
        {
          "intent": "OrgChart-Reports",
          "score": 0.00240071164
        },
        {
          "intent": "Utilities.Help",
          "score": 0.001770991
        },
        {
          "intent": "EmployeeFeedback",
          "score": 0.001697356
        },
        {
          "intent": "OrgChart-Manager",
          "score": 0.00168116146
        },
        {
          "intent": "Utilities.Stop",
          "score": 0.00163952739
        },
        {
          "intent": "FindForm",
          "score": 0.00112958835
        }
      ],
      "entities": [
        {
          "entity": "wayne berry",
          "type": "NewEmployee",
          "startIndex": 5,
          "endIndex": 15,
          "score": 0.629158735
        },
        {
          "entity": "newark",
          "type": "NewEmployeeRelocation",
          "startIndex": 22,
          "endIndex": 27,
          "score": 0.638941
        }
      ]
    }  
    ```

The intent prediction score is only about 50%. If your client application requires a higher number, this needs to be fixed. The entities were not predicted either.

Patterns will help the prediction score, however, the entities must be correctly predicted before the pattern matches the utterance. 

## <a name="add-a-pattern-that-uses-roles"></a>Add a pattern that uses roles
1. Select **Build** in the top navigation.

2. Select **Patterns** in the left navigation.

3. Select **NewEmployeeRelocationProcess** from the **Select an intent** drop-down list. 

4. Enter the following pattern: `move {NewEmployee} from {NewEmployeeRelocation:NewEmployeeReloOrigin} to {NewEmployeeRelocation:NewEmployeeReloDestination}[.]`

    If you train, publish, and query the endpoint, you may be disappointed to see that the entities are not found, so the pattern didn't match, therefore the prediction didn't improve. This is a consequence of not enough example utterances with labeled entities. Instead of adding more examples, add a phrase list to fix this problem.

## <a name="create-a-phrase-list-for-cities"></a>Create a phrase list for Cities
Cities, like people's names are tricky in that they can be any mix of words and punctuation. But the cities of the region and world are known, so LUIS needs a phrase list of cities to begin learning. 

1. Select **Phrase list** from the **Improve app performance** section of the left menu. 

2. Name the list `Cities` and add the following `values` for the list:

    |Values of phrase list|
    |--|
    |Seattle|
    |San Diego|
    |New York City|
    |Los Angeles|
    |Portland|
    |Philadephia|
    |Miami|
    |Dallas|

    Do not add every city in the world or even every city in the region. LUIS needs to be able to generalize what a city is from the list. 

    Make sure to keep **These values are interchangeable** selected. This setting means the words on the list on treated as synonyms. This is exactly how they should be treated in the pattern.

    Remember [the last time](luis-quickstart-primary-and-secondary-data.md) the tutorial series created a phrase list was also to boost entity detection of a simple entity.  

3. Train and publish the app.

## <a name="query-endpoint-for-pattern"></a>Query endpoint for pattern
1. On the **Publish** page, select the **endpoint** link at the bottom of the page. This action opens another browser window with the endpoint URL in the address bar. 

2. Go to the end of the URL in the address and enter `Move wayne berry from miami to mount vernon`. The last querystring parameter is `q`, the utterance **query**. 

    ```JSON
    {
      "query": "Move Wayne Berry from Miami to Mount Vernon",
      "topScoringIntent": {
        "intent": "NewEmployeeRelocationProcess",
        "score": 0.9999999
      },
      "intents": [
        {
          "intent": "NewEmployeeRelocationProcess",
          "score": 0.9999999
        },
        {
          "intent": "Utilities.Confirm",
          "score": 1.49678385E-06
        },
        {
          "intent": "MoveEmployee",
          "score": 8.240291E-07
        },
        {
          "intent": "GetJobInformation",
          "score": 6.3131273E-07
        },
        {
          "intent": "None",
          "score": 4.25E-09
        },
        {
          "intent": "OrgChart-Manager",
          "score": 2.8E-09
        },
        {
          "intent": "OrgChart-Reports",
          "score": 2.8E-09
        },
        {
          "intent": "EmployeeFeedback",
          "score": 1.64E-09
        },
        {
          "intent": "Utilities.StartOver",
          "score": 1.64E-09
        },
        {
          "intent": "Utilities.Help",
          "score": 1.48181822E-09
        },
        {
          "intent": "Utilities.Stop",
          "score": 1.48181822E-09
        },
        {
          "intent": "Utilities.Cancel",
          "score": 1.35E-09
        },
        {
          "intent": "FindForm",
          "score": 1.23846156E-09
        },
        {
          "intent": "ApplyForJob",
          "score": 5.692308E-10
        }
      ],
      "entities": [
        {
          "entity": "wayne berry",
          "type": "builtin.keyPhrase",
          "startIndex": 5,
          "endIndex": 15
        },
        {
          "entity": "miami",
          "type": "builtin.keyPhrase",
          "startIndex": 22,
          "endIndex": 26
        },
        {
          "entity": "wayne berry",
          "type": "NewEmployee",
          "startIndex": 5,
          "endIndex": 15,
          "score": 0.9410646,
          "role": ""
        },
        {
          "entity": "miami",
          "type": "NewEmployeeRelocation",
          "startIndex": 22,
          "endIndex": 26,
          "score": 0.9853915,
          "role": "NewEmployeeReloOrigin"
        },
        {
          "entity": "mount vernon",
          "type": "NewEmployeeRelocation",
          "startIndex": 31,
          "endIndex": 42,
          "score": 0.986044347,
          "role": "NewEmployeeReloDestination"
        }
      ],
      "sentimentAnalysis": {
        "label": "neutral",
        "score": 0.5
      }
}
    ```

The intent score is now much higher and the role names are part of the entity response.

## <a name="clean-up-resources"></a>Clean up resources

[!INCLUDE [LUIS How to clean up resources](../../../includes/cognitive-services-luis-tutorial-how-to-clean-up-resources.md)]

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Learn best practices for LUIS apps](luis-concept-best-practices.md)
