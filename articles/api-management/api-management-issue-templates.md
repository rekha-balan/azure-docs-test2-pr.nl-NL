---
title: Issue templates in Azure API Management | Microsoft Docs
description: Learn how to customize the content of the Issue pages in the developer portal in Azure API Management.
services: api-management
documentationcenter: ''
author: miaojiang
manager: erikre
editor: ''
ms.assetid: 47da4bb2-426e-4e53-8fa7-214ee2e3ab37
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8832a885bbb38cd2c487cf677bb2f7d28fff4e10
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670314"
---
# <a name="issue-templates-in-azure-api-management"></a><span data-ttu-id="7eed9-103">Issue templates in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="7eed9-103">Issue templates in Azure API Management</span></span>
<span data-ttu-id="7eed9-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span><span class="sxs-lookup"><span data-stu-id="7eed9-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="7eed9-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span><span class="sxs-lookup"><span data-stu-id="7eed9-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="7eed9-106">The templates in this section allow you to customize the content of the Issue pages in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="7eed9-106">The templates in this section allow you to customize the content of the Issue pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="7eed9-107">Issue list</span><span class="sxs-lookup"><span data-stu-id="7eed9-107">Issue list</span></span>](#IssueList)  
  
> [!NOTE]
>  <span data-ttu-id="7eed9-108">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span><span class="sxs-lookup"><span data-stu-id="7eed9-108">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="7eed9-109">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span><span class="sxs-lookup"><span data-stu-id="7eed9-109">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="7eed9-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7eed9-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  
  
##  <a name="IssueList"></a> <span data-ttu-id="7eed9-111">Issue list</span><span class="sxs-lookup"><span data-stu-id="7eed9-111">Issue list</span></span>  
 <span data-ttu-id="7eed9-112">The **Issue list** template allows you to customize the body of the issue list page in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="7eed9-112">The **Issue list** template allows you to customize the body of the issue list page in the developer portal.</span></span>  
  
 <span data-ttu-id="7eed9-113">![Issue List Developer Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-issue-templates/apim-issue-list-developer-portal.png "APIM Issue List Developer Portal")</span><span class="sxs-lookup"><span data-stu-id="7eed9-113">![Issue List Developer Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-issue-templates/apim-issue-list-developer-portal.png "APIM Issue List Developer Portal")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="7eed9-114">Default template</span><span class="sxs-lookup"><span data-stu-id="7eed9-114">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-md-9">  
    <h2>{% localized "IssuesStrings|WebIssuesIndexTitle" %}</h2>  
  </div>  
</div>  
<div class="row">  
  <div class="col-md-12">  
    {% if issues.size > 0 %}  
    <ul class="list-unstyled">  
      {% capture reportedBy %}{% localized "IssuesStrings|WebIssuesStatusReportedBy" %}{% endcapture %}  
      {% assign replaceString0 = '{0}' %}  
      {% assign replaceString1 = '{1}' %}  
      {% for issue in issues %}  
      <li>  
        <h3>  
          <a href="/issues/{{issue.id}}">{{issue.title}}</a>  
        </h3>  
        <p>{{issue.description}}</p>  
        <em>  
          {% capture state %}{{issue.issueState}}{% endcapture %}  
          {% capture devName %}{{issue.subscriptionDeveloperName}}{% endcapture %}  
          {% capture str1 %}{{ reportedBy | replace : replaceString0, state }}{% endcapture %}  
          {{ str1 | replace : replaceString1, devName }}  
          <span class="UtcDateElement">{{ issue.reportedOn | date: "r" }}</span>  
        </em>  
      </li>  
      {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    {% if canReportIssue %}  
    <a class="btn btn-primary" id="createIssue" href="/Issues/Create">{% localized "IssuesStrings|WebIssuesReportIssueButton" %}</a>  
    {% elsif isAuthenticated %}  
    <hr />  
    <p>{% localized "IssuesStrings|WebIssuesNoActiveSubscriptions" %}</p>  
    {% else %}  
    <hr />  
    <p>  
      {% capture signIntext %}{% localized "IssuesStrings|WebIssuesNotSignin" %}{% endcapture %}  
      {% capture link %}<a href="/signin">{% localized "IssuesStrings|WebIssuesSignIn" %}</a>{% endcapture %}  
      {{ signIntext | replace : replaceString0, link }}  
    </p>  
    {% endif %}  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="7eed9-115">Controls</span><span class="sxs-lookup"><span data-stu-id="7eed9-115">Controls</span></span>  
 <span data-ttu-id="7eed9-116">The `Issue list` template may use the following [page controls](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="7eed9-116">The `Issue list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="7eed9-117">paging-control</span><span class="sxs-lookup"><span data-stu-id="7eed9-117">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="7eed9-118">Data model</span><span class="sxs-lookup"><span data-stu-id="7eed9-118">Data model</span></span>  
  
|<span data-ttu-id="7eed9-119">Property</span><span class="sxs-lookup"><span data-stu-id="7eed9-119">Property</span></span>|<span data-ttu-id="7eed9-120">Type</span><span class="sxs-lookup"><span data-stu-id="7eed9-120">Type</span></span>|<span data-ttu-id="7eed9-121">Description</span><span class="sxs-lookup"><span data-stu-id="7eed9-121">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="7eed9-122">Issues</span><span class="sxs-lookup"><span data-stu-id="7eed9-122">Issues</span></span>|<span data-ttu-id="7eed9-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span><span class="sxs-lookup"><span data-stu-id="7eed9-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span></span>|<span data-ttu-id="7eed9-124">The issues visible to the current user.</span><span class="sxs-lookup"><span data-stu-id="7eed9-124">The issues visible to the current user.</span></span>|  
|<span data-ttu-id="7eed9-125">Paging</span><span class="sxs-lookup"><span data-stu-id="7eed9-125">Paging</span></span>|<span data-ttu-id="7eed9-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span><span class="sxs-lookup"><span data-stu-id="7eed9-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="7eed9-127">The paging information for the applications collection.</span><span class="sxs-lookup"><span data-stu-id="7eed9-127">The paging information for the applications collection.</span></span>|  
|<span data-ttu-id="7eed9-128">IsAuthenticated</span><span class="sxs-lookup"><span data-stu-id="7eed9-128">IsAuthenticated</span></span>|<span data-ttu-id="7eed9-129">boolean</span><span class="sxs-lookup"><span data-stu-id="7eed9-129">boolean</span></span>|<span data-ttu-id="7eed9-130">Whether the current user is signed-in to the developer portal.</span><span class="sxs-lookup"><span data-stu-id="7eed9-130">Whether the current user is signed-in to the developer portal.</span></span>|  
|<span data-ttu-id="7eed9-131">CanReportIssues</span><span class="sxs-lookup"><span data-stu-id="7eed9-131">CanReportIssues</span></span>|<span data-ttu-id="7eed9-132">boolean</span><span class="sxs-lookup"><span data-stu-id="7eed9-132">boolean</span></span>|<span data-ttu-id="7eed9-133">Whether the current user has permissions to file an issue.</span><span class="sxs-lookup"><span data-stu-id="7eed9-133">Whether the current user has permissions to file an issue.</span></span>|  
|<span data-ttu-id="7eed9-134">Search</span><span class="sxs-lookup"><span data-stu-id="7eed9-134">Search</span></span>|<span data-ttu-id="7eed9-135">string</span><span class="sxs-lookup"><span data-stu-id="7eed9-135">string</span></span>|<span data-ttu-id="7eed9-136">This property is deprecated and should not be used.</span><span class="sxs-lookup"><span data-stu-id="7eed9-136">This property is deprecated and should not be used.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="7eed9-137">Sample template data</span><span class="sxs-lookup"><span data-stu-id="7eed9-137">Sample template data</span></span>  
  
```json  
{  
    "Issues": [  
        {  
            "Id": "5702b68bb16653124c8f9ba7",  
            "ApiId": "570275f1b16653124c8f9ba3",  
            "Title": "I couldn't figure out how to connect my application to the API",  
            "Description": "I'm having trouble connecting my application to the backend API.",  
            "SubscriptionDeveloperName": "Clayton",  
            "IssueState": "Proposed",  
            "ReportedOn": "2016-04-04T18:46:35.64",  
            "Comments": null,  
            "Attachments": null,  
            "Services": null  
        }  
    ],  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "IsAuthenticated": true,  
    "CanReportIssue": true,  
    "Search": null  
}  
```

## <a name="next-steps"></a><span data-ttu-id="7eed9-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="7eed9-138">Next steps</span></span>
<span data-ttu-id="7eed9-139">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7eed9-139">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
