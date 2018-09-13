---
title: Lambda search syntax in the Academic Knowledge API | Microsoft Docs
description: Learn about the Lambda search syntax you can use in the Academic Knowledge API in Microsoft Cognitive Services.
services: cognitive-services
author: alch-msft
manager: kuansanw
ms.service: cognitive-services
ms.technology: academic-knowledge
ms.topic: article
ms.date: 03/23/2017
ms.author: alch
ms.openlocfilehash: e64ad4634f8c1ae4df35f8c2b95972edc405396b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540887"
---
# <a name="lambda-search-syntax"></a><span data-ttu-id="f0235-103">Lambda Search Syntax</span><span class="sxs-lookup"><span data-stu-id="f0235-103">Lambda Search Syntax</span></span>

<span data-ttu-id="f0235-104">Each *lambda* search query string describes a graph pattern.</span><span class="sxs-lookup"><span data-stu-id="f0235-104">Each *lambda* search query string describes a graph pattern.</span></span> <span data-ttu-id="f0235-105">A query must have at least one starting node, specifying from which graph node we start the traversal.</span><span class="sxs-lookup"><span data-stu-id="f0235-105">A query must have at least one starting node, specifying from which graph node we start the traversal.</span></span> <span data-ttu-id="f0235-106">To specify a starting node, call the *MAG.StartFrom()* method and pass in the ID(s) of one or more node(s) or a query object that specifies the search constraints.</span><span class="sxs-lookup"><span data-stu-id="f0235-106">To specify a starting node, call the *MAG.StartFrom()* method and pass in the ID(s) of one or more node(s) or a query object that specifies the search constraints.</span></span> <span data-ttu-id="f0235-107">The *StartFrom()* method has three overloads.</span><span class="sxs-lookup"><span data-stu-id="f0235-107">The *StartFrom()* method has three overloads.</span></span> <span data-ttu-id="f0235-108">All of them take two arguments with the second being optional.</span><span class="sxs-lookup"><span data-stu-id="f0235-108">All of them take two arguments with the second being optional.</span></span> <span data-ttu-id="f0235-109">The first argument can be a long integer, an enumerable collection of long integer, or a string representing a JSON object, with the same semantics as in *json* search:</span><span class="sxs-lookup"><span data-stu-id="f0235-109">The first argument can be a long integer, an enumerable collection of long integer, or a string representing a JSON object, with the same semantics as in *json* search:</span></span>
```
StartFrom(long cellid, IEnumerable<string> select = null)
StartFrom(IEnumerable<long> cellid, IEnumerable<string> select = null)
StartFrom(string queryObject, IEnumerable<string> select = null)
```

<span data-ttu-id="f0235-110">The process of writing a lambda search query is to walk from one node to another.</span><span class="sxs-lookup"><span data-stu-id="f0235-110">The process of writing a lambda search query is to walk from one node to another.</span></span> <span data-ttu-id="f0235-111">To specify the type of the edge to walk through, use *FollowEdge()* and pass in the desired edge types.</span><span class="sxs-lookup"><span data-stu-id="f0235-111">To specify the type of the edge to walk through, use *FollowEdge()* and pass in the desired edge types.</span></span> <span data-ttu-id="f0235-112">*FollowEdge()* takes an arbitrary number of string arguments:</span><span class="sxs-lookup"><span data-stu-id="f0235-112">*FollowEdge()* takes an arbitrary number of string arguments:</span></span>
```
FollowEdge(params string[] edgeTypes)
```
> [!NOTE]
> <span data-ttu-id="f0235-113">If we do not care about the type(s) of the edge(s) to follow, simply omit *FollowEdge()* between two nodes: the query will walk through all the possible edges between these two nodes.</span><span class="sxs-lookup"><span data-stu-id="f0235-113">If we do not care about the type(s) of the edge(s) to follow, simply omit *FollowEdge()* between two nodes: the query will walk through all the possible edges between these two nodes.</span></span>

<span data-ttu-id="f0235-114">We can specify the traversal actions to be taken on a node via *VisitNode()*, that is, whether to stop at this node and return the current path as the result or to continue to explore the graph.</span><span class="sxs-lookup"><span data-stu-id="f0235-114">We can specify the traversal actions to be taken on a node via *VisitNode()*, that is, whether to stop at this node and return the current path as the result or to continue to explore the graph.</span></span>  <span data-ttu-id="f0235-115">The enum type *Action* defines two types of actions: *Action.Return* and *Action.Continue*.</span><span class="sxs-lookup"><span data-stu-id="f0235-115">The enum type *Action* defines two types of actions: *Action.Return* and *Action.Continue*.</span></span> <span data-ttu-id="f0235-116">We can pass such an enum value directly into *VisitNode()*, or combine them with bitwise-and operator '&'.</span><span class="sxs-lookup"><span data-stu-id="f0235-116">We can pass such an enum value directly into *VisitNode()*, or combine them with bitwise-and operator '&'.</span></span> <span data-ttu-id="f0235-117">When two action are combined, it means that both actions will be taken.</span><span class="sxs-lookup"><span data-stu-id="f0235-117">When two action are combined, it means that both actions will be taken.</span></span> <span data-ttu-id="f0235-118">Note: do not use bitwise-or operator '|' on actions.</span><span class="sxs-lookup"><span data-stu-id="f0235-118">Note: do not use bitwise-or operator '|' on actions.</span></span> <span data-ttu-id="f0235-119">Doing so will cause the query to terminate without returning anything.</span><span class="sxs-lookup"><span data-stu-id="f0235-119">Doing so will cause the query to terminate without returning anything.</span></span> <span data-ttu-id="f0235-120">Skipping *VisitNode()* between two *FollowEdge()* calls will cause the query to unconditionally explore the graph after arriving at a node.</span><span class="sxs-lookup"><span data-stu-id="f0235-120">Skipping *VisitNode()* between two *FollowEdge()* calls will cause the query to unconditionally explore the graph after arriving at a node.</span></span>

```
VisitNode(Action action, IEnumerable<string> select = null)
```

<span data-ttu-id="f0235-121">For *VisitNode()*, we can also pass in a lambda expression of type *Expression\<Func\<INode, Action\>\>*, which takes an *INode* and returns a traversal action:</span><span class="sxs-lookup"><span data-stu-id="f0235-121">For *VisitNode()*, we can also pass in a lambda expression of type *Expression\<Func\<INode, Action\>\>*, which takes an *INode* and returns a traversal action:</span></span>

```
VisitNode(Expression<Func<INode, Action>> action, IEnumerable<string> select = null)
```

## <a name="inode"></a><span data-ttu-id="f0235-122">*INode*</span><span class="sxs-lookup"><span data-stu-id="f0235-122">*INode*</span></span> 

<span data-ttu-id="f0235-123">*INode* provides *read-only* data access interfaces and a few built-in helper functions on a node.</span><span class="sxs-lookup"><span data-stu-id="f0235-123">*INode* provides *read-only* data access interfaces and a few built-in helper functions on a node.</span></span> 

### <a name="basic-data-access-interfaces"></a><span data-ttu-id="f0235-124">Basic data access interfaces</span><span class="sxs-lookup"><span data-stu-id="f0235-124">Basic data access interfaces</span></span>

##### <a name="long-cellid"></a><span data-ttu-id="f0235-125">long CellID</span><span class="sxs-lookup"><span data-stu-id="f0235-125">long CellID</span></span>

<span data-ttu-id="f0235-126">The 64-bit ID of the node.</span><span class="sxs-lookup"><span data-stu-id="f0235-126">The 64-bit ID of the node.</span></span> 

##### <a name="t-getfieldtstring-fieldname"></a><span data-ttu-id="f0235-127">T GetField\<T\>(string fieldName)</span><span class="sxs-lookup"><span data-stu-id="f0235-127">T GetField\<T\>(string fieldName)</span></span>

<span data-ttu-id="f0235-128">Gets the value of the specified property.</span><span class="sxs-lookup"><span data-stu-id="f0235-128">Gets the value of the specified property.</span></span> <span data-ttu-id="f0235-129">*T* is the desired type that the field is supposed to be interpreted as.</span><span class="sxs-lookup"><span data-stu-id="f0235-129">*T* is the desired type that the field is supposed to be interpreted as.</span></span> <span data-ttu-id="f0235-130">Automatic type casting will be attempted if the desired type cannot be implicitly converted from the type of the field.</span><span class="sxs-lookup"><span data-stu-id="f0235-130">Automatic type casting will be attempted if the desired type cannot be implicitly converted from the type of the field.</span></span> <span data-ttu-id="f0235-131">Note: when the property is multi-valued, *GetField\<string\>* will cause the list to be serialized to a Json string ["val1", "val2", ...]. If the property does not exist, it will throw an exception and abort the current graph exploration.</span><span class="sxs-lookup"><span data-stu-id="f0235-131">Note: when the property is multi-valued, *GetField\<string\>* will cause the list to be serialized to a Json string ["val1", "val2", ...]. If the property does not exist, it will throw an exception and abort the current graph exploration.</span></span>

##### <a name="bool-containsfieldstring-fieldname"></a><span data-ttu-id="f0235-132">bool ContainsField(string fieldName)</span><span class="sxs-lookup"><span data-stu-id="f0235-132">bool ContainsField(string fieldName)</span></span>

<span data-ttu-id="f0235-133">Tells if a field with the given name exists in the current node.</span><span class="sxs-lookup"><span data-stu-id="f0235-133">Tells if a field with the given name exists in the current node.</span></span>

##### <a name="string-getstring-fieldname"></a><span data-ttu-id="f0235-134">string get(string fieldName)</span><span class="sxs-lookup"><span data-stu-id="f0235-134">string get(string fieldName)</span></span>

<span data-ttu-id="f0235-135">Works like *GetField\<string\>(fieldName)*.</span><span class="sxs-lookup"><span data-stu-id="f0235-135">Works like *GetField\<string\>(fieldName)*.</span></span> <span data-ttu-id="f0235-136">However, it does not throw exceptions when the field is not found, it returns an empty string("") instead.</span><span class="sxs-lookup"><span data-stu-id="f0235-136">However, it does not throw exceptions when the field is not found, it returns an empty string("") instead.</span></span>

##### <a name="bool-hasstring-fieldname"></a><span data-ttu-id="f0235-137">bool has(string fieldName)</span><span class="sxs-lookup"><span data-stu-id="f0235-137">bool has(string fieldName)</span></span>

<span data-ttu-id="f0235-138">Tells if the given property exists in the current node.</span><span class="sxs-lookup"><span data-stu-id="f0235-138">Tells if the given property exists in the current node.</span></span> <span data-ttu-id="f0235-139">Same as *ContainsField(fieldName)*.</span><span class="sxs-lookup"><span data-stu-id="f0235-139">Same as *ContainsField(fieldName)*.</span></span>

##### <a name="bool-hasstring-fieldname-string-value"></a><span data-ttu-id="f0235-140">bool has(string fieldName, string value)</span><span class="sxs-lookup"><span data-stu-id="f0235-140">bool has(string fieldName, string value)</span></span>

<span data-ttu-id="f0235-141">Tells if the property has the given value.</span><span class="sxs-lookup"><span data-stu-id="f0235-141">Tells if the property has the given value.</span></span> 

##### <a name="int-countstring-fieldname"></a><span data-ttu-id="f0235-142">int count(string fieldname)</span><span class="sxs-lookup"><span data-stu-id="f0235-142">int count(string fieldname)</span></span>

<span data-ttu-id="f0235-143">Get the count of values of a given property.</span><span class="sxs-lookup"><span data-stu-id="f0235-143">Get the count of values of a given property.</span></span> <span data-ttu-id="f0235-144">When the property does not exist, returns 0.</span><span class="sxs-lookup"><span data-stu-id="f0235-144">When the property does not exist, returns 0.</span></span>

### <a name="built-in-helper-functions"></a><span data-ttu-id="f0235-145">Built-in Helper Functions</span><span class="sxs-lookup"><span data-stu-id="f0235-145">Built-in Helper Functions</span></span>

##### <a name="action-returnifbool-condition"></a><span data-ttu-id="f0235-146">Action return_if(bool condition)</span><span class="sxs-lookup"><span data-stu-id="f0235-146">Action return_if(bool condition)</span></span>

<span data-ttu-id="f0235-147">Returns *Action.Return* if the condition is *true*.</span><span class="sxs-lookup"><span data-stu-id="f0235-147">Returns *Action.Return* if the condition is *true*.</span></span> <span data-ttu-id="f0235-148">If the condition is *false* and this expression is not joined with other actions by a bitwise-and operator, the graph exploration will be aborted.</span><span class="sxs-lookup"><span data-stu-id="f0235-148">If the condition is *false* and this expression is not joined with other actions by a bitwise-and operator, the graph exploration will be aborted.</span></span>

##### <a name="action-continueifbool-condition"></a><span data-ttu-id="f0235-149">Action continue_if(bool condition)</span><span class="sxs-lookup"><span data-stu-id="f0235-149">Action continue_if(bool condition)</span></span>

<span data-ttu-id="f0235-150">Returns *Action.Continue* if the condition is *true*.</span><span class="sxs-lookup"><span data-stu-id="f0235-150">Returns *Action.Continue* if the condition is *true*.</span></span> <span data-ttu-id="f0235-151">If the condition is *false* and this expression is not joined with other actions by a bitwise-and operator, the graph exploration will be aborted.</span><span class="sxs-lookup"><span data-stu-id="f0235-151">If the condition is *false* and this expression is not joined with other actions by a bitwise-and operator, the graph exploration will be aborted.</span></span>

##### <a name="bool-dicedouble-p"></a><span data-ttu-id="f0235-152">bool dice(double p)</span><span class="sxs-lookup"><span data-stu-id="f0235-152">bool dice(double p)</span></span>

<span data-ttu-id="f0235-153">Generates a random number that is greater than or equal to 0.0 and less than 1.0.</span><span class="sxs-lookup"><span data-stu-id="f0235-153">Generates a random number that is greater than or equal to 0.0 and less than 1.0.</span></span> <span data-ttu-id="f0235-154">This function returns *true* only if the number is less than or equal to *p*.</span><span class="sxs-lookup"><span data-stu-id="f0235-154">This function returns *true* only if the number is less than or equal to *p*.</span></span>

<span data-ttu-id="f0235-155">Compared with *json* search, *lambda* search is more expressive: C# lambda expressions can be directly used to specify query patterns.</span><span class="sxs-lookup"><span data-stu-id="f0235-155">Compared with *json* search, *lambda* search is more expressive: C# lambda expressions can be directly used to specify query patterns.</span></span> <span data-ttu-id="f0235-156">Here are two examples.</span><span class="sxs-lookup"><span data-stu-id="f0235-156">Here are two examples.</span></span>

```
MAG.StartFrom(@"{
    type  : ""ConferenceSeries"",
    match : {
        FullName : ""graph""
    }
}", new List<string>{ "FullName", "ShortName" })
.FollowEdge("ConferenceInstanceIDs")
.VisitNode(v => v.return_if(v.GetField<DateTime>("StartDate").ToString().Contains("2014")),
        new List<string>{ "FullName", "StartDate" })
```

```
MAG.StartFrom(@"{
    type  : ""Affiliation"",
    match : {
        Name : ""microsoft""
    }
}").FollowEdge("PaperIDs")
.VisitNode(v => v.return_if(v.get("NormalizedTitle").Contains("graph") || v.GetField<int>("CitationCount") > 100),
        new List<string>{ "OriginalTitle", "CitationCount" })
```
