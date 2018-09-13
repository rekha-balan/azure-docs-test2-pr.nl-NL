---
title: User profile templates in Azure API Management | Microsoft Docs
description: Learn how to customize the content of the User Profile pages in the developer portal in Azure API Management.
services: api-management
documentationcenter: ''
author: miaojiang
manager: erikre
editor: ''
ms.assetid: 2e3b73ef-d223-44fe-9280-c3af3fd4a030
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 7ccfd5047e814d769993d978e6bbec16da33314d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548885"
---
# <a name="user-profile-templates-in-azure-api-management"></a><span data-ttu-id="a30fd-103">User profile templates in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="a30fd-103">User profile templates in Azure API Management</span></span>
<span data-ttu-id="a30fd-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span><span class="sxs-lookup"><span data-stu-id="a30fd-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="a30fd-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span><span class="sxs-lookup"><span data-stu-id="a30fd-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="a30fd-106">The templates in this section allow you to customize the content of the User profile pages in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="a30fd-106">The templates in this section allow you to customize the content of the User profile pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="a30fd-107">Profile</span><span class="sxs-lookup"><span data-stu-id="a30fd-107">Profile</span></span>](#Profile)  
  
-   [<span data-ttu-id="a30fd-108">Subscriptions</span><span class="sxs-lookup"><span data-stu-id="a30fd-108">Subscriptions</span></span>](#Subscriptions)  
  
-   [<span data-ttu-id="a30fd-109">Applications</span><span class="sxs-lookup"><span data-stu-id="a30fd-109">Applications</span></span>](#Applications)  
  
-   [<span data-ttu-id="a30fd-110">Update account info</span><span class="sxs-lookup"><span data-stu-id="a30fd-110">Update account info</span></span>](#UpdateAccountInfo)  
  
> [!NOTE]
>  <span data-ttu-id="a30fd-111">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span><span class="sxs-lookup"><span data-stu-id="a30fd-111">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="a30fd-112">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span><span class="sxs-lookup"><span data-stu-id="a30fd-112">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="a30fd-113">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="a30fd-113">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <a name="Profile"></a> <span data-ttu-id="a30fd-114">Profile</span><span class="sxs-lookup"><span data-stu-id="a30fd-114">Profile</span></span>  
 <span data-ttu-id="a30fd-115">The **profile** template allows you to customize the user profile section of the user profile page in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="a30fd-115">The **profile** template allows you to customize the user profile section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="a30fd-116">![User Profile Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-user-profile-templates/apim-user-profile-page.png "APIM User Profile Page")</span><span class="sxs-lookup"><span data-stu-id="a30fd-116">![User Profile Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-user-profile-templates/apim-user-profile-page.png "APIM User Profile Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="a30fd-117">Default template</span><span class="sxs-lookup"><span data-stu-id="a30fd-117">Default template</span></span>  
  
```xml  
<div class="pull-right">  
  {% if canChangePassword == true %}  
  <a class="btn btn-default" id="ChangePassword" role="button" href="{{changePasswordUrl}}">{% localized "UserProfile|ButtonLabelChangePassword" %}</a>  
  {% endif %}  
  <a id="changeAccountInfo" href="{{changeNameOrEmailUrl}}" class="btn btn-default">  
    <span class="glyphicon glyphicon-user"></span>  
    <span>{% localized "UserProfile|ButtonLabelChangeAccountInfo" %}</span>  
  </a>  
</div>  
<h2>{% localized "SubscriptionStrings|PageTitleDeveloperProfile" %}</h2>  
<div class="container-fluid">  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="Email">{% localized "UserProfile|TextboxLabelEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="Email">{{email}}</div>  
  </div>  
  
  {% if isSystemUser != true %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="FirstName">{% localized "UserProfile|TextboxLabelEmailFirstName" %}</label>  
    </div>  
    <div class="col-sm-9" id="FirstName">{{FirstName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="LastName">{% localized "UserProfile|TextboxLabelEmailLastName" %}</label>  
    </div>  
    <div class="col-sm-9" id="LastName">{{LastName}}</div>  
  </div>  
  {% else %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="CompanyName">{% localized "UserProfile|TextboxLabelOrganizationName" %}</label>  
    </div>  
    <div class="col-sm-9" id="CompanyName">{{CompanyName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="AddresserEmail">{% localized "UserProfile|TextboxLabelNotificationsSenderEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="AddresserEmail">{{AddresserEmail}}</div>  
  </div>  
  {% endif %}  
  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="a30fd-118">Controls</span><span class="sxs-lookup"><span data-stu-id="a30fd-118">Controls</span></span>  
 <span data-ttu-id="a30fd-119">This template may not use any [page controls](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="a30fd-119">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="a30fd-120">Data model</span><span class="sxs-lookup"><span data-stu-id="a30fd-120">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="a30fd-121">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span><span class="sxs-lookup"><span data-stu-id="a30fd-121">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="a30fd-122">Property</span><span class="sxs-lookup"><span data-stu-id="a30fd-122">Property</span></span>|<span data-ttu-id="a30fd-123">Type</span><span class="sxs-lookup"><span data-stu-id="a30fd-123">Type</span></span>|<span data-ttu-id="a30fd-124">Description</span><span class="sxs-lookup"><span data-stu-id="a30fd-124">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="a30fd-125">firstName</span><span class="sxs-lookup"><span data-stu-id="a30fd-125">firstName</span></span>|<span data-ttu-id="a30fd-126">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-126">string</span></span>|<span data-ttu-id="a30fd-127">First name of the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-127">First name of the current user.</span></span>|  
|<span data-ttu-id="a30fd-128">lastName</span><span class="sxs-lookup"><span data-stu-id="a30fd-128">lastName</span></span>|<span data-ttu-id="a30fd-129">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-129">string</span></span>|<span data-ttu-id="a30fd-130">Last name of the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-130">Last name of the current user.</span></span>|  
|<span data-ttu-id="a30fd-131">companyName</span><span class="sxs-lookup"><span data-stu-id="a30fd-131">companyName</span></span>|<span data-ttu-id="a30fd-132">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-132">string</span></span>|<span data-ttu-id="a30fd-133">The company name of the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-133">The company name of the current user.</span></span>|  
|<span data-ttu-id="a30fd-134">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="a30fd-134">addresserEmail</span></span>|<span data-ttu-id="a30fd-135">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-135">string</span></span>|<span data-ttu-id="a30fd-136">Email address of the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-136">Email address of the current user.</span></span>|  
|<span data-ttu-id="a30fd-137">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="a30fd-137">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="a30fd-138">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-138">string</span></span>|<span data-ttu-id="a30fd-139">Relative URL to view analytics for the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-139">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="a30fd-140">subscriptions</span><span class="sxs-lookup"><span data-stu-id="a30fd-140">subscriptions</span></span>|<span data-ttu-id="a30fd-141">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span><span class="sxs-lookup"><span data-stu-id="a30fd-141">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="a30fd-142">The subscriptions for the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-142">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="a30fd-143">applications</span><span class="sxs-lookup"><span data-stu-id="a30fd-143">applications</span></span>|<span data-ttu-id="a30fd-144">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span><span class="sxs-lookup"><span data-stu-id="a30fd-144">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="a30fd-145">The applications of the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-145">The applications of the current user.</span></span>|  
|<span data-ttu-id="a30fd-146">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="a30fd-146">changePasswordUrl</span></span>|<span data-ttu-id="a30fd-147">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-147">string</span></span>|<span data-ttu-id="a30fd-148">The relative URL to change the current user's password.</span><span class="sxs-lookup"><span data-stu-id="a30fd-148">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="a30fd-149">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="a30fd-149">changeNameOrEmailUrl</span></span>|<span data-ttu-id="a30fd-150">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-150">string</span></span>|<span data-ttu-id="a30fd-151">The relative URL to change the name and email for the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-151">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="a30fd-152">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="a30fd-152">canChangePassword</span></span>|<span data-ttu-id="a30fd-153">boolean</span><span class="sxs-lookup"><span data-stu-id="a30fd-153">boolean</span></span>|<span data-ttu-id="a30fd-154">Whether the current user can change their password.</span><span class="sxs-lookup"><span data-stu-id="a30fd-154">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="a30fd-155">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="a30fd-155">isSystemUser</span></span>|<span data-ttu-id="a30fd-156">boolean</span><span class="sxs-lookup"><span data-stu-id="a30fd-156">boolean</span></span>|<span data-ttu-id="a30fd-157">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="a30fd-157">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="a30fd-158">Sample template data</span><span class="sxs-lookup"><span data-stu-id="a30fd-158">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <a name="Subscriptions"></a> <span data-ttu-id="a30fd-159">Subscriptions</span><span class="sxs-lookup"><span data-stu-id="a30fd-159">Subscriptions</span></span>  
 <span data-ttu-id="a30fd-160">The **Subscriptions** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="a30fd-160">The **Subscriptions** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="a30fd-161">![User Subscription Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-user-profile-templates/apim-user-subscription-page.png "APIM User Subscription Page")</span><span class="sxs-lookup"><span data-stu-id="a30fd-161">![User Subscription Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-user-profile-templates/apim-user-subscription-page.png "APIM User Subscription Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="a30fd-162">Default template</span><span class="sxs-lookup"><span data-stu-id="a30fd-162">Default template</span></span>  
  
```xml  
<div class="ap-account-subscriptions">  
  <a href="{{developersUsageStatisticsLink}}" id="UsageStatistics" class="btn btn-default pull-right">  
    <span class="glyphicon glyphicon-stats"></span>  
    <span>{% localized "SubscriptionListStrings|WebDevelopersUsageStatisticsLink" %}</span>  
  </a>  
  
  <h2>{% localized "SubscriptionListStrings|WebDevelopersYourSubscriptions" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th>Subscription details</th>  
        <th>Product</th>  
        <th>{% localized "SubscriptionListStrings|WebDevelopersSubscriptionTableStateHeader" %}</th>  
        <th>Action</th>  
      </tr>  
    </thead>  
    <tbody>  
      {% if subscriptions.size == 0 %}  
      <tr>  
        <td class="text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
      {% else %}  
      {% for subscription in subscriptions %}  
      <tr id="{{subscription.id}}" {% if subscription.hasExpired %} class="expired" {% endif %}>  
        <td>  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelName" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.displayName }}  
            </div>  
            <div class="col-lg-2">  
              <a class="btn-link" href="/Subscriptions/{{subscription.id}}/Rename">Rename</a>  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          {% if subscription.isAwaitingApproval %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelRequestedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.createdDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% else %}  
          {% if subscription.isRejected == false %}  
          {% if subscription.startDate %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelStartedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.startDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% endif %}  
  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.primaryKey}}', '{{subscription.id}}', true) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersPrimaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="primary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <!-- ko if: !requestInProgress() -->  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="togglePrimary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel"></a>  
                |  
                <a href="#" class="btn-link" id="regeneratePrimary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel"></a>  
              </div>  
              <!-- /ko -->  
              <!-- ko if: requestInProgress() -->  
              <div class="progress progress-striped active">  
                <div class="progress-bar" role="progressbar" aria-valuenow="100" aria-valuemin="0" aria-valuemax="100" style="width: 100%">  
                  <span class="sr-only"></span>  
                </div>  
              </div>  
              <!-- /ko -->  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          <!-- /ko -->  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.secondaryKey}}', '{{subscription.id}}', false) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersSecondaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="secondary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="toggleSecondary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel">{% localized "SubscriptionListStrings|ButtonLabelShowKey" %}</a>  
                |  
                <a href="#" class="btn-link" id="regenerateSecondary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel">{% localized "SubscriptionListStrings|WebDevelopersRegenerateLink" %}</a>  
              </div>  
            </div>  
            <div class="clearfix"> </div>  
          </div>  
          <!-- /ko -->  
          {% endif %}  
          {% endif %}  
        </td>  
        <td>  
          <a href="{{subscription.productDetailsUrl}}">{{subscription.productTitle}}</a>  
        </td>  
        <td>  
          <strong>  
            {{subscription.state}}  
          </strong>  
        </td>  
        <td>  
          <div class="nowrap">  
            {% if subscription.canBeCancelled %}  
            <subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }"></subscription-cancel>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="a30fd-163">Controls</span><span class="sxs-lookup"><span data-stu-id="a30fd-163">Controls</span></span>  
 <span data-ttu-id="a30fd-164">This template may use the following [page controls](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="a30fd-164">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="a30fd-165">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="a30fd-165">subscription-cancel</span></span>](api-management-page-controls.md#subscription-cancel)  
  
### <a name="data-model"></a><span data-ttu-id="a30fd-166">Data model</span><span class="sxs-lookup"><span data-stu-id="a30fd-166">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="a30fd-167">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span><span class="sxs-lookup"><span data-stu-id="a30fd-167">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="a30fd-168">Property</span><span class="sxs-lookup"><span data-stu-id="a30fd-168">Property</span></span>|<span data-ttu-id="a30fd-169">Type</span><span class="sxs-lookup"><span data-stu-id="a30fd-169">Type</span></span>|<span data-ttu-id="a30fd-170">Description</span><span class="sxs-lookup"><span data-stu-id="a30fd-170">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="a30fd-171">firstName</span><span class="sxs-lookup"><span data-stu-id="a30fd-171">firstName</span></span>|<span data-ttu-id="a30fd-172">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-172">string</span></span>|<span data-ttu-id="a30fd-173">First name of the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-173">First name of the current user.</span></span>|  
|<span data-ttu-id="a30fd-174">lastName</span><span class="sxs-lookup"><span data-stu-id="a30fd-174">lastName</span></span>|<span data-ttu-id="a30fd-175">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-175">string</span></span>|<span data-ttu-id="a30fd-176">Last name of the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-176">Last name of the current user.</span></span>|  
|<span data-ttu-id="a30fd-177">companyName</span><span class="sxs-lookup"><span data-stu-id="a30fd-177">companyName</span></span>|<span data-ttu-id="a30fd-178">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-178">string</span></span>|<span data-ttu-id="a30fd-179">The company name of the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-179">The company name of the current user.</span></span>|  
|<span data-ttu-id="a30fd-180">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="a30fd-180">addresserEmail</span></span>|<span data-ttu-id="a30fd-181">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-181">string</span></span>|<span data-ttu-id="a30fd-182">Email address of the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-182">Email address of the current user.</span></span>|  
|<span data-ttu-id="a30fd-183">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="a30fd-183">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="a30fd-184">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-184">string</span></span>|<span data-ttu-id="a30fd-185">Relative URL to view analytics for the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-185">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="a30fd-186">subscriptions</span><span class="sxs-lookup"><span data-stu-id="a30fd-186">subscriptions</span></span>|<span data-ttu-id="a30fd-187">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span><span class="sxs-lookup"><span data-stu-id="a30fd-187">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="a30fd-188">The subscriptions for the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-188">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="a30fd-189">applications</span><span class="sxs-lookup"><span data-stu-id="a30fd-189">applications</span></span>|<span data-ttu-id="a30fd-190">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span><span class="sxs-lookup"><span data-stu-id="a30fd-190">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="a30fd-191">The applications of the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-191">The applications of the current user.</span></span>|  
|<span data-ttu-id="a30fd-192">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="a30fd-192">changePasswordUrl</span></span>|<span data-ttu-id="a30fd-193">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-193">string</span></span>|<span data-ttu-id="a30fd-194">The relative URL to change the current user's password.</span><span class="sxs-lookup"><span data-stu-id="a30fd-194">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="a30fd-195">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="a30fd-195">changeNameOrEmailUrl</span></span>|<span data-ttu-id="a30fd-196">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-196">string</span></span>|<span data-ttu-id="a30fd-197">The relative URL to change the name and email for the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-197">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="a30fd-198">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="a30fd-198">canChangePassword</span></span>|<span data-ttu-id="a30fd-199">boolean</span><span class="sxs-lookup"><span data-stu-id="a30fd-199">boolean</span></span>|<span data-ttu-id="a30fd-200">Whether the current user can change their password.</span><span class="sxs-lookup"><span data-stu-id="a30fd-200">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="a30fd-201">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="a30fd-201">isSystemUser</span></span>|<span data-ttu-id="a30fd-202">boolean</span><span class="sxs-lookup"><span data-stu-id="a30fd-202">boolean</span></span>|<span data-ttu-id="a30fd-203">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="a30fd-203">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="a30fd-204">Sample template data</span><span class="sxs-lookup"><span data-stu-id="a30fd-204">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <a name="Applications"></a> <span data-ttu-id="a30fd-205">Applications</span><span class="sxs-lookup"><span data-stu-id="a30fd-205">Applications</span></span>  
 <span data-ttu-id="a30fd-206">The **Applications** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="a30fd-206">The **Applications** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="a30fd-207">![User Account Applications Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-user-profile-templates/apim-user-account-applications-page.png "APIM User Account Applications Page")</span><span class="sxs-lookup"><span data-stu-id="a30fd-207">![User Account Applications Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-user-profile-templates/apim-user-account-applications-page.png "APIM User Account Applications Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="a30fd-208">Default template</span><span class="sxs-lookup"><span data-stu-id="a30fd-208">Default template</span></span>  
  
```xml  
<div class="ap-account-applications">  
  <a id="RegisterApplication" href="/Developer/Applications/Register" class="btn btn-success pull-right">  
    <span class="glyphicon glyphicon-plus"></span>  
    <span>{% localized "ApplicationListStrings|WebDevelopersRegisterAppLink" %}</span>  
  </a>  
  <h2>{% localized "ApplicationListStrings|WebDevelopersYourApplicationsHeader" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th class="col-md-8">{% localized "ApplicationListStrings|WebDevelopersAppTableNameHeader" %}</th>  
        <th class="col-md-2">{% localized "ApplicationListStrings|WebDevelopersAppTableCategoryHeader" %}</th>  
        <th class="col-md-2" colspan="2">{% localized "ApplicationListStrings|WebDevelopersAppTableStateHeader" %}</th>  
      </tr>  
    </thead>  
    <tbody>  
  
      {% if applications.size == 0 %}  
  
      <tr>  
        <td class="col-md-12 text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
  
      {% else %}  
  
      {% for app in applications %}  
      <tr>  
        <td class="col-md-8">  
          {{app.title}}  
        </td>  
        <td class="col-md-2">  
          {{app.categoryName}}  
        </td>  
        <td class="col-md-2">  
          <strong>  
            {% case app.state %}  
            {% when ApplicationStateModel.Registered %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotSubminted" %}  
  
            {% when ApplicationStateModel.Unpublished %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotPublished" %}  
  
            {% else %}  
            {{ app.state }}  
            {% endcase %}  
          </strong>  
        </td>  
        <td class="col-md-1">  
          <div class="nowrap">  
            {% if app.state != ApplicationStateModel.Submitted and app.state != ApplicationStateModel.Published %}  
            <app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="a30fd-209">Controls</span><span class="sxs-lookup"><span data-stu-id="a30fd-209">Controls</span></span>  
 <span data-ttu-id="a30fd-210">This template may use the following [page controls](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="a30fd-210">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="a30fd-211">app-actions</span><span class="sxs-lookup"><span data-stu-id="a30fd-211">app-actions</span></span>](api-management-page-controls.md#app-actions)  
  
### <a name="data-model"></a><span data-ttu-id="a30fd-212">Data model</span><span class="sxs-lookup"><span data-stu-id="a30fd-212">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="a30fd-213">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span><span class="sxs-lookup"><span data-stu-id="a30fd-213">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="a30fd-214">Property</span><span class="sxs-lookup"><span data-stu-id="a30fd-214">Property</span></span>|<span data-ttu-id="a30fd-215">Type</span><span class="sxs-lookup"><span data-stu-id="a30fd-215">Type</span></span>|<span data-ttu-id="a30fd-216">Description</span><span class="sxs-lookup"><span data-stu-id="a30fd-216">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="a30fd-217">firstName</span><span class="sxs-lookup"><span data-stu-id="a30fd-217">firstName</span></span>|<span data-ttu-id="a30fd-218">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-218">string</span></span>|<span data-ttu-id="a30fd-219">First name of the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-219">First name of the current user.</span></span>|  
|<span data-ttu-id="a30fd-220">lastName</span><span class="sxs-lookup"><span data-stu-id="a30fd-220">lastName</span></span>|<span data-ttu-id="a30fd-221">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-221">string</span></span>|<span data-ttu-id="a30fd-222">Last name of the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-222">Last name of the current user.</span></span>|  
|<span data-ttu-id="a30fd-223">companyName</span><span class="sxs-lookup"><span data-stu-id="a30fd-223">companyName</span></span>|<span data-ttu-id="a30fd-224">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-224">string</span></span>|<span data-ttu-id="a30fd-225">The company name of the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-225">The company name of the current user.</span></span>|  
|<span data-ttu-id="a30fd-226">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="a30fd-226">addresserEmail</span></span>|<span data-ttu-id="a30fd-227">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-227">string</span></span>|<span data-ttu-id="a30fd-228">Email address of the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-228">Email address of the current user.</span></span>|  
|<span data-ttu-id="a30fd-229">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="a30fd-229">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="a30fd-230">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-230">string</span></span>|<span data-ttu-id="a30fd-231">Relative URL to view analytics for the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-231">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="a30fd-232">subscriptions</span><span class="sxs-lookup"><span data-stu-id="a30fd-232">subscriptions</span></span>|<span data-ttu-id="a30fd-233">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span><span class="sxs-lookup"><span data-stu-id="a30fd-233">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="a30fd-234">The subscriptions for the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-234">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="a30fd-235">applications</span><span class="sxs-lookup"><span data-stu-id="a30fd-235">applications</span></span>|<span data-ttu-id="a30fd-236">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span><span class="sxs-lookup"><span data-stu-id="a30fd-236">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="a30fd-237">The applications of the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-237">The applications of the current user.</span></span>|  
|<span data-ttu-id="a30fd-238">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="a30fd-238">changePasswordUrl</span></span>|<span data-ttu-id="a30fd-239">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-239">string</span></span>|<span data-ttu-id="a30fd-240">The relative URL to change the current user's password.</span><span class="sxs-lookup"><span data-stu-id="a30fd-240">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="a30fd-241">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="a30fd-241">changeNameOrEmailUrl</span></span>|<span data-ttu-id="a30fd-242">string</span><span class="sxs-lookup"><span data-stu-id="a30fd-242">string</span></span>|<span data-ttu-id="a30fd-243">The relative URL to change the name and email for the current user.</span><span class="sxs-lookup"><span data-stu-id="a30fd-243">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="a30fd-244">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="a30fd-244">canChangePassword</span></span>|<span data-ttu-id="a30fd-245">boolean</span><span class="sxs-lookup"><span data-stu-id="a30fd-245">boolean</span></span>|<span data-ttu-id="a30fd-246">Whether the current user can change their password.</span><span class="sxs-lookup"><span data-stu-id="a30fd-246">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="a30fd-247">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="a30fd-247">isSystemUser</span></span>|<span data-ttu-id="a30fd-248">boolean</span><span class="sxs-lookup"><span data-stu-id="a30fd-248">boolean</span></span>|<span data-ttu-id="a30fd-249">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="a30fd-249">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="a30fd-250">Sample template data</span><span class="sxs-lookup"><span data-stu-id="a30fd-250">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <a name="UpdateAccountInfo"></a> <span data-ttu-id="a30fd-251">Update account info</span><span class="sxs-lookup"><span data-stu-id="a30fd-251">Update account info</span></span>  
 <span data-ttu-id="a30fd-252">The **Uodate account info** template allows you to customize the **Update account information** page in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="a30fd-252">The **Uodate account info** template allows you to customize the **Update account information** page in the developer portal.</span></span>  
  
 <span data-ttu-id="a30fd-253">![User Account Info Page Developer Portal Templates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-user-profile-templates/apim-user-account-info-page-developer-portal-templates.png "APIM User Account Info Page Developer Portal Templates")</span><span class="sxs-lookup"><span data-stu-id="a30fd-253">![User Account Info Page Developer Portal Templates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-user-profile-templates/apim-user-account-info-page-developer-portal-templates.png "APIM User Account Info Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="a30fd-254">Default template</span><span class="sxs-lookup"><span data-stu-id="a30fd-254">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-sm-6 col-md-6">  
    <div class="form-group">  
      <label for="Email">{% localized "SigninResources|TextboxLabelEmail" %}</label>  
      <input autofocus="autofocus" class="form-control" id="Email" name="Email" type="text" value="{{email}}">  
    </div>  
    <div class="form-group">  
      <label for="FirstName">{% localized "SigninResources|TextboxLabelEmailFirstName" %}</label>  
      <input class="form-control" id="FirstName" name="FirstName" type="text" value="{{firstName}}">  
    </div>  
    <div class="form-group">  
      <label for="LastName">{% localized "SigninResources|TextboxLabelEmailLastName" %}</label>  
      <input class="form-control" id="LastName" name="LastName" type="text" value="{{lastName}}">  
    </div>  
    <div class="form-group">  
      <label for="Password">{% localized "SigninResources|WebAuthenticationSigninPasswordLabel" %}</label>  
      <input class="form-control" id="Password" name="Password" type="password">  
    </div>  
  </div>  
</div>  
  
<button type="submit" class="btn btn-primary" id="UpdateProfile">  
  {% localized "UpdateProfileStrings|ButtonLabelUpdateProfile" %}  
</button>  
<a class="btn btn-default" href="/developer" role="button">  
  {% localized "CommonStrings|ButtonLabelCancel" %}  
</a>  
```  
  
### <a name="controls"></a><span data-ttu-id="a30fd-255">Controls</span><span class="sxs-lookup"><span data-stu-id="a30fd-255">Controls</span></span>  
 <span data-ttu-id="a30fd-256">This template may not use any [page controls](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="a30fd-256">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="a30fd-257">Data model</span><span class="sxs-lookup"><span data-stu-id="a30fd-257">Data model</span></span>  
 <span data-ttu-id="a30fd-258">[User account info](api-management-template-data-model-reference.md#UserAccountInfo) entity.</span><span class="sxs-lookup"><span data-stu-id="a30fd-258">[User account info](api-management-template-data-model-reference.md#UserAccountInfo) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="a30fd-259">Sample template data</span><span class="sxs-lookup"><span data-stu-id="a30fd-259">Sample template data</span></span>  
  
```json  
{  
    "FirstName": "Administrator",  
    "LastName": "",  
    "Email": "admin@live.com",  
    "Password": null,  
    "NameIdentifier": null,  
    "ProviderName": null,  
    "IsBasicAccount": false  
}  
```

## <a name="next-steps"></a><span data-ttu-id="a30fd-260">Next steps</span><span class="sxs-lookup"><span data-stu-id="a30fd-260">Next steps</span></span>
<span data-ttu-id="a30fd-261">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a30fd-261">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>



