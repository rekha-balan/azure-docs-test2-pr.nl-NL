---
title: Application templates in Azure API Management | Microsoft Docs
description: Learn how to customize the content of the Application pages in the developer portal in Azure API Management.
services: api-management
documentationcenter: ''
author: miaojiang
manager: erikre
editor: ''
ms.assetid: f3122c4d-e10e-4cdf-977b-36e8f4133fc8
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 7d8b3085797f310a14a9d313d18648c7e6cbbd0c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553102"
---
# <a name="application-templates-in-azure-api-management"></a><span data-ttu-id="07b0e-103">Application templates in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="07b0e-103">Application templates in Azure API Management</span></span>
<span data-ttu-id="07b0e-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span><span class="sxs-lookup"><span data-stu-id="07b0e-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="07b0e-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span><span class="sxs-lookup"><span data-stu-id="07b0e-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="07b0e-106">The templates in this section allow you to customize the content of the Application pages in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="07b0e-106">The templates in this section allow you to customize the content of the Application pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="07b0e-107">Application list</span><span class="sxs-lookup"><span data-stu-id="07b0e-107">Application list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="07b0e-108">Application</span><span class="sxs-lookup"><span data-stu-id="07b0e-108">Application</span></span>](#Application)  
  
> [!NOTE]
>  <span data-ttu-id="07b0e-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span><span class="sxs-lookup"><span data-stu-id="07b0e-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="07b0e-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span><span class="sxs-lookup"><span data-stu-id="07b0e-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="07b0e-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="07b0e-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <a name="ProductList"></a> <span data-ttu-id="07b0e-112">Application list</span><span class="sxs-lookup"><span data-stu-id="07b0e-112">Application list</span></span>  
 <span data-ttu-id="07b0e-113">The **Application list** template allows you to customize the body of the application list page in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="07b0e-113">The **Application list** template allows you to customize the body of the application list page in the developer portal.</span></span>  
  
 <span data-ttu-id="07b0e-114">![Application List Page Developer Portal Templates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-application-templates/apim-application-list-page-developer-portal-templates.png "APIM Application List Page Developer Portal Templates")</span><span class="sxs-lookup"><span data-stu-id="07b0e-114">![Application List Page Developer Portal Templates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-application-templates/apim-application-list-page-developer-portal-templates.png "APIM Application List Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="07b0e-115">Default template</span><span class="sxs-lookup"><span data-stu-id="07b0e-115">Default template</span></span>  
  
```xml  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "AppStrings|WebApplicationsHeader" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if applications.size > 0 %}  
        <ul class="list-unstyled">  
        {% for app in applications %}  
            <li>  
            {% if app.application.icon.url != "" %}  
                <aside>  
                    <a href="/applications/details/{{app.application.id}}"><img src="{{app.application.icon.url}}" alt="App Icon" /></a>  
                </aside>  
            {% endif %}  
                <h3><a href="/applications/details/{{app.application.id}}">{{app.application.title}}</a></h3>  
                {{app.application.description}}  
            </li>     
        {% endfor %}  
        </ul>  
        <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="07b0e-116">Controls</span><span class="sxs-lookup"><span data-stu-id="07b0e-116">Controls</span></span>  
 <span data-ttu-id="07b0e-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="07b0e-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="07b0e-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="07b0e-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="07b0e-119">Data model</span><span class="sxs-lookup"><span data-stu-id="07b0e-119">Data model</span></span>  
  
|<span data-ttu-id="07b0e-120">Property</span><span class="sxs-lookup"><span data-stu-id="07b0e-120">Property</span></span>|<span data-ttu-id="07b0e-121">Type</span><span class="sxs-lookup"><span data-stu-id="07b0e-121">Type</span></span>|<span data-ttu-id="07b0e-122">Description</span><span class="sxs-lookup"><span data-stu-id="07b0e-122">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="07b0e-123">Paging</span><span class="sxs-lookup"><span data-stu-id="07b0e-123">Paging</span></span>|<span data-ttu-id="07b0e-124">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span><span class="sxs-lookup"><span data-stu-id="07b0e-124">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="07b0e-125">The paging information for the applications collection.</span><span class="sxs-lookup"><span data-stu-id="07b0e-125">The paging information for the applications collection.</span></span>|  
|<span data-ttu-id="07b0e-126">Applications</span><span class="sxs-lookup"><span data-stu-id="07b0e-126">Applications</span></span>|<span data-ttu-id="07b0e-127">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span><span class="sxs-lookup"><span data-stu-id="07b0e-127">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="07b0e-128">The applications visible to the current user.</span><span class="sxs-lookup"><span data-stu-id="07b0e-128">The applications visible to the current user.</span></span>|  
|<span data-ttu-id="07b0e-129">CategoryName</span><span class="sxs-lookup"><span data-stu-id="07b0e-129">CategoryName</span></span>|<span data-ttu-id="07b0e-130">string</span><span class="sxs-lookup"><span data-stu-id="07b0e-130">string</span></span>|<span data-ttu-id="07b0e-131">The category of application.</span><span class="sxs-lookup"><span data-stu-id="07b0e-131">The category of application.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="07b0e-132">Sample template data</span><span class="sxs-lookup"><span data-stu-id="07b0e-132">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Applications": [  
        {  
            "Application": {  
                "Id": "5702b96fb16653124c8f9ba8",  
                "Title": "Contoso Calculator",  
                "Description": "A simple online calculator.",  
                "Url": null,  
                "Version": null,  
                "Requirements": "Free application with no requirements.",  
                "State": 2,  
                "RegistrationDate": "2016-04-04T18:59:00",  
                "CategoryId": 5,  
                "DeveloperId": "5702b5b0b16653124c8f9ba4",  
                "Attachments": [  
                    {  
                        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                        "Type": "Icon",  
                        "ContentType": "image/png"  
                    },  
                    {  
                        "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
                        "Type": "Screenshot",  
                        "ContentType": "image/png"  
                    }  
                ],  
                "Icon": {  
                    "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                    "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                    "Type": "Icon",  
                    "ContentType": "image/png"  
                }  
            },  
            "CategoryName": "Finance"  
        }  
    ]  
}  
```  
  
##  <a name="Application"></a> <span data-ttu-id="07b0e-133">Application</span><span class="sxs-lookup"><span data-stu-id="07b0e-133">Application</span></span>  
 <span data-ttu-id="07b0e-134">The **Application** template allows you to customize the body of the application page in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="07b0e-134">The **Application** template allows you to customize the body of the application page in the developer portal.</span></span>  
  
 <span data-ttu-id="07b0e-135">![Application Page Developer Portal Templates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-application-templates/apim-application-page-developer-portal-templates.png "APIM Application Page Developer Portal Templates")</span><span class="sxs-lookup"><span data-stu-id="07b0e-135">![Application Page Developer Portal Templates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-application-templates/apim-application-page-developer-portal-templates.png "APIM Application Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="07b0e-136">Default template</span><span class="sxs-lookup"><span data-stu-id="07b0e-136">Default template</span></span>  
  
```xml  
<h2>{{title}}</h2>  
{% if icon.url != "" %}  
<aside class="applications_aside">  
  <div class="image-placeholder">  
    <img src="{{icon.url}}" alt="Application Icon" />  
  </div>  
</aside>  
{% endif %}  
  
<article>  
  {% if url != "" %}  
    <a target="_blank" href="{{url}}">{{url}}</a>  
  {% endif %}  
  
  <p>{{description}}</p>  
  
  {% if requirements != null %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsRequirementsHeader" %}</h3>  
  <p>{{requirements}}</p>  
  {% endif %}  
  
  {% if attachments.size > 0 %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsScreenshotsHeader" %}</h3>  
    {% for screenshot in attachments %}  
      {% if screenshot.type != "Icon" %}  
      <a href="{{screenshot.url}}" data-lightbox="example-set">  
          <img src="/Developer/Applications/Thumbnail?url={{screenshot.url}}" alt='{% localized "AppDetailsStrings|WebApplicationsScreenshotAlt" %}' />  
      </a>  
      {% endif %}  
    {% endfor %}  
  {% endif %}  
</article>  
  
```  
  
### <a name="controls"></a><span data-ttu-id="07b0e-137">Controls</span><span class="sxs-lookup"><span data-stu-id="07b0e-137">Controls</span></span>  
 <span data-ttu-id="07b0e-138">The `Application` template does not allow the use of any [page controls](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="07b0e-138">The `Application` template does not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="07b0e-139">Data model</span><span class="sxs-lookup"><span data-stu-id="07b0e-139">Data model</span></span>  
 <span data-ttu-id="07b0e-140">[Application](api-management-template-data-model-reference.md#Application) entity.</span><span class="sxs-lookup"><span data-stu-id="07b0e-140">[Application](api-management-template-data-model-reference.md#Application) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="07b0e-141">Sample template data</span><span class="sxs-lookup"><span data-stu-id="07b0e-141">Sample template data</span></span>  
  
```json  
{  
    "Id": "5702b96fb16653124c8f9ba8",  
    "Title": "Contoso Calculator",  
    "Description": "A simple online calculator.",  
    "Url": null,  
    "Version": null,  
    "Requirements": "Free application with no requirements.",  
    "State": 2,  
    "RegistrationDate": "2016-04-04T18:59:00",  
    "CategoryId": 5,  
    "DeveloperId": "5702b5b0b16653124c8f9ba4",  
    "Attachments": [  
        {  
            "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
            "Type": "Icon",  
            "ContentType": "image/png"  
        },  
        {  
            "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
            "Type": "Screenshot",  
            "ContentType": "image/png"  
        }  
    ],  
    "Icon": {  
        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
        "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
        "Type": "Icon",  
        "ContentType": "image/png"  
    }  
}  
```

## <a name="next-steps"></a><span data-ttu-id="07b0e-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="07b0e-142">Next steps</span></span>
<span data-ttu-id="07b0e-143">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="07b0e-143">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>

