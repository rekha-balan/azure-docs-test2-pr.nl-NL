---
title: Data operation samples - Azure Logic Apps | Microsoft Docs
description: Code samples for data operation action definitions in Azure Logic Apps
services: logic-apps
ms.service: logic-apps
author: ecfan
ms.author: estfan
manager: jeconnoc
ms.topic: reference
ms.date: 07/25/2018
ms.reviewer: klam, LADocs
ms.suite: integration
ms.openlocfilehash: 79f4792a65b2c79caeffc660978ff3ebd2dae7b8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866828"
---
# <a name="data-operation-code-samples-for-azure-logic-apps"></a><span data-ttu-id="0e2c7-103">Data operation code samples for Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="0e2c7-103">Data operation code samples for Azure Logic Apps</span></span>

<span data-ttu-id="0e2c7-104">Here are the code samples for the data operation action definitions in the article, [Perform data operations](../logic-apps/logic-apps-perform-data-operations.md).</span><span class="sxs-lookup"><span data-stu-id="0e2c7-104">Here are the code samples for the data operation action definitions in the article, [Perform data operations](../logic-apps/logic-apps-perform-data-operations.md).</span></span> <span data-ttu-id="0e2c7-105">You can use these samples for when you want to try the examples with your own logic app's underlying workflow definition, Azure subscription, and API connections.</span><span class="sxs-lookup"><span data-stu-id="0e2c7-105">You can use these samples for when you want to try the examples with your own logic app's underlying workflow definition, Azure subscription, and API connections.</span></span> <span data-ttu-id="0e2c7-106">Just copy and paste these action definitions into the code view editor for your logic app's workflow definition, and then modify the definitions for your specific workflow.</span><span class="sxs-lookup"><span data-stu-id="0e2c7-106">Just copy and paste these action definitions into the code view editor for your logic app's workflow definition, and then modify the definitions for your specific workflow.</span></span> 

<span data-ttu-id="0e2c7-107">Based on JavaScript Object Notation (JSON) standards, these action definitions appear in alphabetical order.</span><span class="sxs-lookup"><span data-stu-id="0e2c7-107">Based on JavaScript Object Notation (JSON) standards, these action definitions appear in alphabetical order.</span></span> <span data-ttu-id="0e2c7-108">However, in the Logic App Designer, each definition appears in the correct sequence within your workflow because each action definition's `runAfter` property specifies the run order.</span><span class="sxs-lookup"><span data-stu-id="0e2c7-108">However, in the Logic App Designer, each definition appears in the correct sequence within your workflow because each action definition's `runAfter` property specifies the run order.</span></span> 

<a name="compose-action-example"></a>

## <a name="compose"></a><span data-ttu-id="0e2c7-109">Compose</span><span class="sxs-lookup"><span data-stu-id="0e2c7-109">Compose</span></span>

<span data-ttu-id="0e2c7-110">To try the [**Compose** action example](../logic-apps/logic-apps-perform-data-operations.md#compose-action), here are the action definitions you can use:</span><span class="sxs-lookup"><span data-stu-id="0e2c7-110">To try the [**Compose** action example](../logic-apps/logic-apps-perform-data-operations.md#compose-action), here are the action definitions you can use:</span></span>

```json
"actions": {
  "Compose": {
    "type": "Compose",
    "inputs": {
      "age": "@variables('ageVar')",
      "fullName": "@{variables('lastNameVar')}, @{variables('firstNameVar')}"
    },
    "runAfter": {
      "Initialize_variable_-_ageVar": [
          "Succeeded"
      ]
    }
  },
  "Initialize_variable_-_ageVar": {
    "type": "InitializeVariable",
    "inputs": {
      "variables": [
        {
          "name": "ageVar",
          "type": "Integer",
          "value": 35
        }
      ]
    },
    "runAfter": {
      "Initialize_variable_-_lastNameVar": [
        "Succeeded"
      ]
    }
  },
  "Initialize_variable_-_firstNameVar": {
    "type": "InitializeVariable",
    "inputs": {
      "variables": [
        {
          "name": "firstNameVar",
          "type": "String",
          "value": "Sophie "
        }
      ]
    },
    "runAfter": {}
  },
  "Initialize_variable_-_lastNameVar": {
    "type": "InitializeVariable",
    "inputs": {
      "variables": [
        {
          "name": "lastNameVar",
          "type": "String",
          "value": "Owen"
        }
      ]
    },
    "runAfter": {
      "Initialize_variable_-_firstNameVar": [
        "Succeeded"
      ]
    }
  }
},
```

<a name="create-csv-table-action-example"></a>

## <a name="create-csv-table"></a><span data-ttu-id="0e2c7-111">Create CSV table</span><span class="sxs-lookup"><span data-stu-id="0e2c7-111">Create CSV table</span></span>

<span data-ttu-id="0e2c7-112">To try the [**Create CSV table** action example](../logic-apps/logic-apps-perform-data-operations.md#create-csv-table-action), here are the action definitions you can use:</span><span class="sxs-lookup"><span data-stu-id="0e2c7-112">To try the [**Create CSV table** action example](../logic-apps/logic-apps-perform-data-operations.md#create-csv-table-action), here are the action definitions you can use:</span></span>

```json
"actions": {
   "Create_CSV_table": {
      "type": "Table",     
      "inputs": {
         "format": "CSV",
         "from": "@variables('myJSONArray')"
      },
      "runAfter": {
         "Initialize_variable_-_JSON_array": [
            "Succeeded"
         ]
      }
   },
   "Initialize_variable_-_JSON_array": {
      "type": "InitializeVariable",
      "inputs": {
         "variables": [ 
            {
               "name": "myJSONArray",
               "type": "Array",
                  "value": [
                     {
                        "Description": "Apples",
                        "Product_ID": 1
                     },
                     {
                        "Description": "Oranges",
                        "Product_ID": 2
                     }
                  ]
            }
         ]
      },
      "runAfter": {}
   }
},
```

<a name="create-html-table-action-example"></a>

## <a name="create-html-table"></a><span data-ttu-id="0e2c7-113">Create HTML table</span><span class="sxs-lookup"><span data-stu-id="0e2c7-113">Create HTML table</span></span>

<span data-ttu-id="0e2c7-114">To try the [**Create HTML table** action example](../logic-apps/logic-apps-perform-data-operations.md#create-html-table-action), here are the action definitions you can use:</span><span class="sxs-lookup"><span data-stu-id="0e2c7-114">To try the [**Create HTML table** action example](../logic-apps/logic-apps-perform-data-operations.md#create-html-table-action), here are the action definitions you can use:</span></span>

```json
"actions": {
   "Create_HTML_table": {
      "type": "Table",     
      "inputs": {
         "format": "HTML",
         "from": "@variables('myJSONArray')"
      },
      "runAfter": {
         "Initialize_variable_-_JSON_array": [
            "Succeeded"
         ]
      }
   },
   "Initialize_variable_-_JSON_array": {
      "type": "InitializeVariable",
      "inputs": {
         "variables": [ 
            {
               "name": "myJSONArray",
               "type": "Array",
                  "value": [
                     {
                        "Description": "Apples",
                        "Product_ID": 1
                     },
                     {
                        "Description": "Oranges",
                        "Product_ID": 2
                     }
                  ]
            }
         ]
      },
      "runAfter": {}
   }
},
```

<a name="filter-array-action-example"></a>

## <a name="filter-array"></a><span data-ttu-id="0e2c7-115">Filter array</span><span class="sxs-lookup"><span data-stu-id="0e2c7-115">Filter array</span></span>

<span data-ttu-id="0e2c7-116">To try the [**Filter array** action example](../logic-apps/logic-apps-perform-data-operations.md#filter-array-action), here are the action definitions you can use:</span><span class="sxs-lookup"><span data-stu-id="0e2c7-116">To try the [**Filter array** action example](../logic-apps/logic-apps-perform-data-operations.md#filter-array-action), here are the action definitions you can use:</span></span>

```json
"actions": {
   "Filter_array": {
      "type": "Query",
      "inputs": {
         "from": "@variables('myIntegerArray')",
         "where": "@greater(item(), 1)"
      },
      "runAfter": {
         "Initialize_variable_-_integer_array": [
            "Succeeded"
         ]
      }
   },
   "Initialize_variable_-_integer_array": {
      "type": "InitializeVariable",
      "inputs": {
         "variables": [ 
            {
               "name": "myIntegerArray",
               "type": "Array",
               "value": [
                  1,
                  2,
                  3,
                  4
               ]
            }
         ]
      },
      "runAfter": {}
   }
},
```

<a name="join-action-example"></a>

## <a name="join"></a><span data-ttu-id="0e2c7-117">Join</span><span class="sxs-lookup"><span data-stu-id="0e2c7-117">Join</span></span>

<span data-ttu-id="0e2c7-118">To try the [**Join** action example](../logic-apps/logic-apps-perform-data-operations.md#join-action), here are the action definitions you can use:</span><span class="sxs-lookup"><span data-stu-id="0e2c7-118">To try the [**Join** action example](../logic-apps/logic-apps-perform-data-operations.md#join-action), here are the action definitions you can use:</span></span>

```json
"actions": {
   "Initialize_variable_-_integer_array": {
      "type": "InitializeVariable",
      "inputs": {
         "variables": [ 
            {
               "name": "myIntegerArray",
               "type": "Array",
               "value": [
                  1,
                  2,
                  3,
                  4
               ]
            }
         ]
      },
      "runAfter": {}
   },
   "Join": {
      "type": "Join",
      "inputs": {
         "from": "@variables('myIntegerArray')",
         "joinWith": ":"
      },
      "runAfter": {
         "Initialize_variable_-_integer_array": [
             "Succeeded"
         ]
      }
   }
},
```

<a name="parse-json-action-example"></a>

## <a name="parse-json"></a><span data-ttu-id="0e2c7-119">Parse JSON</span><span class="sxs-lookup"><span data-stu-id="0e2c7-119">Parse JSON</span></span>

<span data-ttu-id="0e2c7-120">To try the [**Parse JSON** action example](../logic-apps/logic-apps-perform-data-operations.md#parse-json-action), here are the action definitions you can use:</span><span class="sxs-lookup"><span data-stu-id="0e2c7-120">To try the [**Parse JSON** action example](../logic-apps/logic-apps-perform-data-operations.md#parse-json-action), here are the action definitions you can use:</span></span>

```json
"actions": {
   "Initialize_variable_-_JSON_object": {
      "type": "InitializeVariable",
      "inputs": {
         "variables": [
            {
               "name": "myJSONObject",
               "type": "Object",
               "value": {
                  "Member": {
                     "Email": "Sophie.Owen@contoso.com",
                     "FirstName": "Sophie",
                     "LastName": "Owen"
                  }
               }
            }
         ]
      },
      "runAfter": {}
   },
   "Parse_JSON": {
      "type": "ParseJson",
      "inputs": {
         "content": "@variables('myJSONObject')",
         "schema": {
            "type": "object",
            "properties": {
               "Member": {
                  "type": "object",
                  "properties": {
                     "Email": {
                        "type": "string"
                     },
                     "FirstName": {
                        "type": "string"
                     },
                     "LastName": {
                        "type": "string"
                     }
                  }
               }
            }
         }
      },
      "runAfter": {
         "Initialize_variable_-_JSON_object": [
            "Succeeded"
         ]
      }
},
```

<a name="select-action-example"></a>

## <a name="select"></a><span data-ttu-id="0e2c7-121">Select</span><span class="sxs-lookup"><span data-stu-id="0e2c7-121">Select</span></span>

<span data-ttu-id="0e2c7-122">To try the [**Select** action example](../logic-apps/logic-apps-perform-data-operations.md#select-action), here are the action definitions you can use:</span><span class="sxs-lookup"><span data-stu-id="0e2c7-122">To try the [**Select** action example](../logic-apps/logic-apps-perform-data-operations.md#select-action), here are the action definitions you can use:</span></span>

```json
"actions": {
   "Initialize_variable_-_integer_array": {
      "type": "InitializeVariable",
      "inputs": {
         "variables": [ 
            {
               "name": "myIntegerArray",
               "type": "Array",
               "value": [
                  1,
                  2,
                  3,
                  4
               ]
            }
         ]
      },
      "runAfter": {}
   },
   "Select": {
      "type": "Select",
      "inputs": {
         "from": "@variables('myIntegerArray')",
         "select": {
            "Product_ID": "@item()"
         }
      },
      "runAfter": {
         "Initialize_variable_-_integer_array": [
           "Succeeded"
         ]
      }
   }
},
```

## <a name="get-support"></a><span data-ttu-id="0e2c7-123">Get support</span><span class="sxs-lookup"><span data-stu-id="0e2c7-123">Get support</span></span>

* <span data-ttu-id="0e2c7-124">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="0e2c7-124">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="0e2c7-125">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="0e2c7-125">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e2c7-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="0e2c7-126">Next steps</span></span>

* [<span data-ttu-id="0e2c7-127">Perform data operations</span><span class="sxs-lookup"><span data-stu-id="0e2c7-127">Perform data operations</span></span>](../logic-apps/logic-apps-perform-data-operations.md)
