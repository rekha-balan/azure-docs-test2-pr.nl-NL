---
title: User, session, and event analysis in Azure Application Insights | Microsoft docs
description: Demographic analysis of users of your web app.
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: conceptual
ms.date: 01/24/2018
ms.reviewer: daviste
ms.author: mbullwin
ms.openlocfilehash: 2bc10a292855832b7ddb9b8e3a59fbe0f17d8dc6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869870"
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a>Users, sessions, and events analysis in Application Insights

Find out when people use your web app, what pages they're most interested in, where your users are located, and what browsers and operating systems they use. Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).

![Screenshot of Application Insights Users](./media/app-insights-usage-segmentation/0001-users.png)

## <a name="get-started"></a>Get started

If you don't yet see data in the users, sessions, or events blades in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).

## <a name="the-users-sessions-and-events-segmentation-tool"></a>The Users, Sessions, and Events segmentation tool

Three of the usage blades use the same tool to slice and dice telemetry from your web app from three perspectives. By filtering and splitting the data, you can uncover insights about the relative usage of different pages and features.

* **Users tool**: How many people used your app and its features.  Users are counted by using anonymous IDs stored in browser cookies. A single person using different browsers or machines will be counted as more than one user.
* **Sessions tool**: How many sessions of user activity have included certain pages and features of your app. A session is counted after half an hour of user inactivity, or after 24 hours of continuous use.
* **Events tool**: How often certain pages and features of your app are used. A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md). 

    A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or the completion of some task. You insert code in your app to [generate custom events](app-insights-api-custom-events-metrics.md#trackevent).

## <a name="querying-for-certain-users"></a>Querying for certain users

Explore different groups of users by adjusting the query options at the top of the Users tool:

* Show: Choose a cohort of users to analyze.
* Who used: Choose custom events and page views.
* During: Choose a time range.
* By: Choose how to bucket the data, either by a period of time or by another property such as browser or city.
* Split By: Choose a property by which to split or segment the data. 
* Add Filters: Limit the query to certain users, sessions, or events based on their properties, such as browser or city. 
 
## <a name="saving-and-sharing-reports"></a>Saving and sharing reports 
You can save Users reports, either private just to you in the My Reports section, or shared with everyone else with access to this Application Insights resource in the Shared Reports section.

To share a link to a Users, Sessions, or Events report; click **Share** in the toolbar, then copy the link.

To share a copy of the data in a Users, Sessions, or Events report; click **Share** in the toolbar, then click the **Word icon** to create a Word document with the data. Or, click the **Word icon** above the main chart.

## <a name="meet-your-users"></a>Meet your users

The **Meet your users** section shows information about five sample users matched by the current query. Considering and exploring the behaviors of individuals, in addition to aggregates, can provide insights about how people actually use your app.

## <a name="next-steps"></a>Next steps

- To enable usage experiences, start sending [custom events](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- If you already send custom events or page views, explore the Usage tools to learn how users use your service.
    - [Funnels](usage-funnels.md)
    - [Retention](app-insights-usage-retention.md)
    - [User Flows](app-insights-usage-flows.md)
    - [Workbooks](app-insights-usage-workbooks.md)
    - [Add user context](app-insights-usage-send-user-context.md)