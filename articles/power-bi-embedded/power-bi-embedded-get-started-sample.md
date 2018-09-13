---
title: Get started with a sample
description: Power BI Embedded, use SDK to add interactive Power BI reports into your business intelligence application
services: power-bi-embedded
documentationcenter: ''
author: guyinacube
manager: erikre
editor: ''
tags: ''
ms.assetid: d8a9ef78-ad4e-4bc7-9711-89172dc5c548
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/02/2017
ms.author: asaxton
ms.openlocfilehash: 3da77241a101e55364caa1b8857a832051b468c3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669375"
---
# <a name="get-started-with-power-bi-embedded-sample"></a><span data-ttu-id="efeff-103">Get started with Power BI Embedded sample</span><span class="sxs-lookup"><span data-stu-id="efeff-103">Get started with Power BI Embedded sample</span></span>

<span data-ttu-id="efeff-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span><span class="sxs-lookup"><span data-stu-id="efeff-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span> <span data-ttu-id="efeff-105">In this article, we'll introduce you to the **Power BI Embedded** get started sample.</span><span class="sxs-lookup"><span data-stu-id="efeff-105">In this article, we'll introduce you to the **Power BI Embedded** get started sample.</span></span>

<span data-ttu-id="efeff-106">Before we go any further, you'll probably want to save the following resources.</span><span class="sxs-lookup"><span data-stu-id="efeff-106">Before we go any further, you'll probably want to save the following resources.</span></span> <span data-ttu-id="efeff-107">They'll help you when integrating Power BI reports into the sample app and your own apps too.</span><span class="sxs-lookup"><span data-stu-id="efeff-107">They'll help you when integrating Power BI reports into the sample app and your own apps too.</span></span>

* [<span data-ttu-id="efeff-108">Sample workspace web app</span><span class="sxs-lookup"><span data-stu-id="efeff-108">Sample workspace web app</span></span>](http://go.microsoft.com/fwlink/?LinkId=761493)
* [<span data-ttu-id="efeff-109">Power BI Embedded API reference</span><span class="sxs-lookup"><span data-stu-id="efeff-109">Power BI Embedded API reference</span></span>](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* <span data-ttu-id="efeff-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span><span class="sxs-lookup"><span data-stu-id="efeff-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span></span>
* [<span data-ttu-id="efeff-111">JavaScript Report Embed Sample</span><span class="sxs-lookup"><span data-stu-id="efeff-111">JavaScript Report Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> <span data-ttu-id="efeff-112">Before you can configure and run the Power BI Embedded get started sample, you need to create at least one **Workspace Collection** in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="efeff-112">Before you can configure and run the Power BI Embedded get started sample, you need to create at least one **Workspace Collection** in your Azure subscription.</span></span> <span data-ttu-id="efeff-113">To learn how to create a **Workspace Collection** in the Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="efeff-113">To learn how to create a **Workspace Collection** in the Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="configure-the-sample-app"></a><span data-ttu-id="efeff-114">Configure the sample app</span><span class="sxs-lookup"><span data-stu-id="efeff-114">Configure the sample app</span></span>

<span data-ttu-id="efeff-115">Let's walk through setting up your Visual Studio development environment to access the  components needed to run the sample app.</span><span class="sxs-lookup"><span data-stu-id="efeff-115">Let's walk through setting up your Visual Studio development environment to access the  components needed to run the sample app.</span></span>

1. <span data-ttu-id="efeff-116">Download and unzip the [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span><span class="sxs-lookup"><span data-stu-id="efeff-116">Download and unzip the [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span></span>
2. <span data-ttu-id="efeff-117">Open **PowerBI-embedded.sln** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="efeff-117">Open **PowerBI-embedded.sln** in Visual Studio.</span></span> <span data-ttu-id="efeff-118">You may need to execute the **Update-Package** command in the NuGET Package Manager Console in order to update the packages used in this solution.</span><span class="sxs-lookup"><span data-stu-id="efeff-118">You may need to execute the **Update-Package** command in the NuGET Package Manager Console in order to update the packages used in this solution.</span></span>
3. <span data-ttu-id="efeff-119">Build the solution.</span><span class="sxs-lookup"><span data-stu-id="efeff-119">Build the solution.</span></span>
4. <span data-ttu-id="efeff-120">Run the **ProvisionSample** console app.</span><span class="sxs-lookup"><span data-stu-id="efeff-120">Run the **ProvisionSample** console app.</span></span> <span data-ttu-id="efeff-121">In the sample console app, you provision a workspace and import a PBIX file.</span><span class="sxs-lookup"><span data-stu-id="efeff-121">In the sample console app, you provision a workspace and import a PBIX file.</span></span>
5. <span data-ttu-id="efeff-122">To provision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span><span class="sxs-lookup"><span data-stu-id="efeff-122">To provision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span></span>
6. <span data-ttu-id="efeff-123">To import a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span><span class="sxs-lookup"><span data-stu-id="efeff-123">To import a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span></span>

7. <span data-ttu-id="efeff-124">Enter your **Workspace Collection** name, and **Access Key**.</span><span class="sxs-lookup"><span data-stu-id="efeff-124">Enter your **Workspace Collection** name, and **Access Key**.</span></span> <span data-ttu-id="efeff-125">You can get these in the **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="efeff-125">You can get these in the **Azure Portal**.</span></span> <span data-ttu-id="efeff-126">To learn more about how to get your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="efeff-126">To learn more about how to get your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/powerbi-embedded-get-started-sample/azure-portal.png)
8. <span data-ttu-id="efeff-127">Copy and save the newly created **Workspace ID** to use later in this article.</span><span class="sxs-lookup"><span data-stu-id="efeff-127">Copy and save the newly created **Workspace ID** to use later in this article.</span></span> <span data-ttu-id="efeff-128">After the **Workspace ID** is created, you can find it the **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="efeff-128">After the **Workspace ID** is created, you can find it the **Azure Portal**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/powerbi-embedded-get-started-sample/workspace-id.png)
9. <span data-ttu-id="efeff-129">To import a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span><span class="sxs-lookup"><span data-stu-id="efeff-129">To import a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span></span> <span data-ttu-id="efeff-130">If you don't have a PBIX file handy, you can download the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="efeff-130">If you don't have a PBIX file handy, you can download the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>
10. <span data-ttu-id="efeff-131">If prompted, enter a friendly name for your **Dataset**.</span><span class="sxs-lookup"><span data-stu-id="efeff-131">If prompted, enter a friendly name for your **Dataset**.</span></span>

<span data-ttu-id="efeff-132">You should see a response like:</span><span class="sxs-lookup"><span data-stu-id="efeff-132">You should see a response like:</span></span>

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> <span data-ttu-id="efeff-133">If your PBIX file contains any direct query connections, run option 7 to update the connection strings.</span><span class="sxs-lookup"><span data-stu-id="efeff-133">If your PBIX file contains any direct query connections, run option 7 to update the connection strings.</span></span>

<span data-ttu-id="efeff-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span><span class="sxs-lookup"><span data-stu-id="efeff-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span></span> <span data-ttu-id="efeff-135">Now, let's look at how to run the **Power BI Embedded** get started sample web app.</span><span class="sxs-lookup"><span data-stu-id="efeff-135">Now, let's look at how to run the **Power BI Embedded** get started sample web app.</span></span>

## <a name="run-the-sample-web-app"></a><span data-ttu-id="efeff-136">Run the sample web app</span><span class="sxs-lookup"><span data-stu-id="efeff-136">Run the sample web app</span></span>
<span data-ttu-id="efeff-137">The web app sample is a sample application that renders reports imported into your **Workspace**.</span><span class="sxs-lookup"><span data-stu-id="efeff-137">The web app sample is a sample application that renders reports imported into your **Workspace**.</span></span> <span data-ttu-id="efeff-138">Here's how to configure the web app sample.</span><span class="sxs-lookup"><span data-stu-id="efeff-138">Here's how to configure the web app sample.</span></span>

1. <span data-ttu-id="efeff-139">In the **PowerBI-embedded** Visual Studio solution, right click the **EmbedSample** web application, and choose **Set as StartUp project**.</span><span class="sxs-lookup"><span data-stu-id="efeff-139">In the **PowerBI-embedded** Visual Studio solution, right click the **EmbedSample** web application, and choose **Set as StartUp project**.</span></span>
2. <span data-ttu-id="efeff-140">In **web.config**, in the **EmbedSample** web application, edit the **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span><span class="sxs-lookup"><span data-stu-id="efeff-140">In **web.config**, in the **EmbedSample** web application, edit the **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span></span>

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. <span data-ttu-id="efeff-141">Run the **EmbedSample** web application.</span><span class="sxs-lookup"><span data-stu-id="efeff-141">Run the **EmbedSample** web application.</span></span>

<span data-ttu-id="efeff-142">Once you run the **EmbedSample** web application, the left navigation panel should contain a **Reports** menu.</span><span class="sxs-lookup"><span data-stu-id="efeff-142">Once you run the **EmbedSample** web application, the left navigation panel should contain a **Reports** menu.</span></span> <span data-ttu-id="efeff-143">To view the report you imported, expand **Reports**, and click a report.</span><span class="sxs-lookup"><span data-stu-id="efeff-143">To view the report you imported, expand **Reports**, and click a report.</span></span> <span data-ttu-id="efeff-144">If you imported the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), the sample web app would look like this:</span><span class="sxs-lookup"><span data-stu-id="efeff-144">If you imported the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), the sample web app would look like this:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

<span data-ttu-id="efeff-145">After you click a report, the **EmbedSample** web application should look something this:</span><span class="sxs-lookup"><span data-stu-id="efeff-145">After you click a report, the **EmbedSample** web application should look something this:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-the-sample-code"></a><span data-ttu-id="efeff-146">Explore the sample code</span><span class="sxs-lookup"><span data-stu-id="efeff-146">Explore the sample code</span></span>

<span data-ttu-id="efeff-147">The **Microsoft Power BI Embedded** sample is an example web app that shows you how to integrate **Power BI** reports into your app.</span><span class="sxs-lookup"><span data-stu-id="efeff-147">The **Microsoft Power BI Embedded** sample is an example web app that shows you how to integrate **Power BI** reports into your app.</span></span> <span data-ttu-id="efeff-148">It uses a Model-View-Controller (MVC) design pattern to demonstrate best practices.</span><span class="sxs-lookup"><span data-stu-id="efeff-148">It uses a Model-View-Controller (MVC) design pattern to demonstrate best practices.</span></span> <span data-ttu-id="efeff-149">This section highlights parts of the sample code that you can explore within the **PowerBI-embedded** web app solution.</span><span class="sxs-lookup"><span data-stu-id="efeff-149">This section highlights parts of the sample code that you can explore within the **PowerBI-embedded** web app solution.</span></span> <span data-ttu-id="efeff-150">The Model-View-Controller (MVC) pattern separates the modeling of the domain, the presentation, and the actions based on user input into three separate classes: Model, View, and Control.</span><span class="sxs-lookup"><span data-stu-id="efeff-150">The Model-View-Controller (MVC) pattern separates the modeling of the domain, the presentation, and the actions based on user input into three separate classes: Model, View, and Control.</span></span> <span data-ttu-id="efeff-151">To learn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span><span class="sxs-lookup"><span data-stu-id="efeff-151">To learn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span></span>

<span data-ttu-id="efeff-152">The **Microsoft Power BI Embedded** sample code is separated as follows.</span><span class="sxs-lookup"><span data-stu-id="efeff-152">The **Microsoft Power BI Embedded** sample code is separated as follows.</span></span> <span data-ttu-id="efeff-153">Each section includes the file name in the PowerBI-embedded.sln solution so that you can easily find the code in the sample.</span><span class="sxs-lookup"><span data-stu-id="efeff-153">Each section includes the file name in the PowerBI-embedded.sln solution so that you can easily find the code in the sample.</span></span>

> [!NOTE]
> <span data-ttu-id="efeff-154">This section is a summary of the sample code that shows how the code was written.</span><span class="sxs-lookup"><span data-stu-id="efeff-154">This section is a summary of the sample code that shows how the code was written.</span></span> <span data-ttu-id="efeff-155">To view the complete sample, please load the PowerBI-embedded.sln solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="efeff-155">To view the complete sample, please load the PowerBI-embedded.sln solution in Visual Studio.</span></span>

### <a name="model"></a><span data-ttu-id="efeff-156">Model</span><span class="sxs-lookup"><span data-stu-id="efeff-156">Model</span></span>

<span data-ttu-id="efeff-157">The sample has a **ReportsViewModel** and **ReportViewModel**.</span><span class="sxs-lookup"><span data-stu-id="efeff-157">The sample has a **ReportsViewModel** and **ReportViewModel**.</span></span>

<span data-ttu-id="efeff-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span><span class="sxs-lookup"><span data-stu-id="efeff-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span></span>

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

<span data-ttu-id="efeff-159">**ReportViewModel.cs**: Represents a Power BI Report.</span><span class="sxs-lookup"><span data-stu-id="efeff-159">**ReportViewModel.cs**: Represents a Power BI Report.</span></span>

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a><span data-ttu-id="efeff-160">Connection string</span><span class="sxs-lookup"><span data-stu-id="efeff-160">Connection string</span></span>

<span data-ttu-id="efeff-161">The connection string must be in the following format:</span><span class="sxs-lookup"><span data-stu-id="efeff-161">The connection string must be in the following format:</span></span>

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

<span data-ttu-id="efeff-162">Using common server and database attributes will fail.</span><span class="sxs-lookup"><span data-stu-id="efeff-162">Using common server and database attributes will fail.</span></span> <span data-ttu-id="efeff-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span><span class="sxs-lookup"><span data-stu-id="efeff-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span></span>

### <a name="view"></a><span data-ttu-id="efeff-164">View</span><span class="sxs-lookup"><span data-stu-id="efeff-164">View</span></span>

<span data-ttu-id="efeff-165">The **View** manages the display of Power BI **Reports** and a Power BI **Report**.</span><span class="sxs-lookup"><span data-stu-id="efeff-165">The **View** manages the display of Power BI **Reports** and a Power BI **Report**.</span></span>

<span data-ttu-id="efeff-166">**Reports.cshtml**: Iterate over **Model.Reports** to create an **ActionLink**.</span><span class="sxs-lookup"><span data-stu-id="efeff-166">**Reports.cshtml**: Iterate over **Model.Reports** to create an **ActionLink**.</span></span> <span data-ttu-id="efeff-167">The **ActionLink** is composed as follows:</span><span class="sxs-lookup"><span data-stu-id="efeff-167">The **ActionLink** is composed as follows:</span></span>

| <span data-ttu-id="efeff-168">Part</span><span class="sxs-lookup"><span data-stu-id="efeff-168">Part</span></span> | <span data-ttu-id="efeff-169">Description</span><span class="sxs-lookup"><span data-stu-id="efeff-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="efeff-170">Title</span><span class="sxs-lookup"><span data-stu-id="efeff-170">Title</span></span> |<span data-ttu-id="efeff-171">Name of the Report.</span><span class="sxs-lookup"><span data-stu-id="efeff-171">Name of the Report.</span></span> |
| <span data-ttu-id="efeff-172">QueryString</span><span class="sxs-lookup"><span data-stu-id="efeff-172">QueryString</span></span> |<span data-ttu-id="efeff-173">A link to the Report ID.</span><span class="sxs-lookup"><span data-stu-id="efeff-173">A link to the Report ID.</span></span> |

    <div id="reports-nav" class="panel-collapse collapse">
        <div class="panel-body">
            <ul class="nav navbar-nav">
                @foreach (var report in Model.Reports)
                {
                    var reportClass = Request.QueryString["reportId"] == report.Id ? "active" : "";
                    <li class="@reportClass">
                        @Html.ActionLink(report.Name, "Report", new { reportId = report.Id })
                    </li>
                }
            </ul>
        </div>
    </div>

<span data-ttu-id="efeff-174">Report.cshtml: Set the **Model.AccessToken**, and the Lambda expression for **PowerBIReportFor**.</span><span class="sxs-lookup"><span data-stu-id="efeff-174">Report.cshtml: Set the **Model.AccessToken**, and the Lambda expression for **PowerBIReportFor**.</span></span>

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a><span data-ttu-id="efeff-175">Controller</span><span class="sxs-lookup"><span data-stu-id="efeff-175">Controller</span></span>

<span data-ttu-id="efeff-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span><span class="sxs-lookup"><span data-stu-id="efeff-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span></span> <span data-ttu-id="efeff-177">A JSON Web Token (JWT) is generated from the **Signing Key** to get the **Credentials**.</span><span class="sxs-lookup"><span data-stu-id="efeff-177">A JSON Web Token (JWT) is generated from the **Signing Key** to get the **Credentials**.</span></span> <span data-ttu-id="efeff-178">The **Credentials** are used to create an instance of **PowerBIClient**.</span><span class="sxs-lookup"><span data-stu-id="efeff-178">The **Credentials** are used to create an instance of **PowerBIClient**.</span></span> <span data-ttu-id="efeff-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span><span class="sxs-lookup"><span data-stu-id="efeff-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span></span>

<span data-ttu-id="efeff-180">CreatePowerBIClient()</span><span class="sxs-lookup"><span data-stu-id="efeff-180">CreatePowerBIClient()</span></span>

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

<span data-ttu-id="efeff-181">ActionResult Reports()</span><span class="sxs-lookup"><span data-stu-id="efeff-181">ActionResult Reports()</span></span>

    public ActionResult Reports()
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = client.Reports.GetReports(this.workspaceCollection, this.workspaceId);

            var viewModel = new ReportsViewModel
            {
                Reports = reportsResponse.Value.ToList()
            };

            return PartialView(viewModel);
        }
    }


<span data-ttu-id="efeff-182">Task<ActionResult> Report(string reportId)</span><span class="sxs-lookup"><span data-stu-id="efeff-182">Task<ActionResult> Report(string reportId)</span></span>

    public async Task<ActionResult> Report(string reportId)
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = await client.Reports.GetReportsAsync(this.workspaceCollection, this.workspaceId);
            var report = reportsResponse.Value.FirstOrDefault(r => r.Id == reportId);
            var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

            var viewModel = new ReportViewModel
            {
                Report = report,
                AccessToken = embedToken.Generate(this.accessKey)
            };

            return View(viewModel);
        }
    }

### <a name="integrate-a-report-into-your-app"></a><span data-ttu-id="efeff-183">Integrate a report into your app</span><span class="sxs-lookup"><span data-stu-id="efeff-183">Integrate a report into your app</span></span>

<span data-ttu-id="efeff-184">Once you have a **Report**, you use an **IFrame** to embed the Power BI **Report**.</span><span class="sxs-lookup"><span data-stu-id="efeff-184">Once you have a **Report**, you use an **IFrame** to embed the Power BI **Report**.</span></span> <span data-ttu-id="efeff-185">Here is a code snippet from  powerbi.js in the **Microsoft Power BI Embedded** sample.</span><span class="sxs-lookup"><span data-stu-id="efeff-185">Here is a code snippet from  powerbi.js in the **Microsoft Power BI Embedded** sample.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a><span data-ttu-id="efeff-186">Filter reports embedded in your application</span><span class="sxs-lookup"><span data-stu-id="efeff-186">Filter reports embedded in your application</span></span>

<span data-ttu-id="efeff-187">You can filter an embedded report using a URL syntax.</span><span class="sxs-lookup"><span data-stu-id="efeff-187">You can filter an embedded report using a URL syntax.</span></span> <span data-ttu-id="efeff-188">To do this, you add a **$filter** query string parameter with an **eq** operator to your iFrame src url with the filter specified.</span><span class="sxs-lookup"><span data-stu-id="efeff-188">To do this, you add a **$filter** query string parameter with an **eq** operator to your iFrame src url with the filter specified.</span></span> <span data-ttu-id="efeff-189">Here is the filter query syntax:</span><span class="sxs-lookup"><span data-stu-id="efeff-189">Here is the filter query syntax:</span></span>

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> <span data-ttu-id="efeff-190">{tableName/fieldName} cannot include spaces or special characters.</span><span class="sxs-lookup"><span data-stu-id="efeff-190">{tableName/fieldName} cannot include spaces or special characters.</span></span> <span data-ttu-id="efeff-191">The {fieldValue} accepts a single categorical value.</span><span class="sxs-lookup"><span data-stu-id="efeff-191">The {fieldValue} accepts a single categorical value.</span></span>  

## <a name="see-also"></a><span data-ttu-id="efeff-192">See also</span><span class="sxs-lookup"><span data-stu-id="efeff-192">See also</span></span>

[<span data-ttu-id="efeff-193">Common Microsoft Power BI Embedded scenarios</span><span class="sxs-lookup"><span data-stu-id="efeff-193">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="efeff-194">Authenticating and authorizing in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="efeff-194">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="efeff-195">Embed a report</span><span class="sxs-lookup"><span data-stu-id="efeff-195">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="efeff-196">Create a new report from a dataset</span><span class="sxs-lookup"><span data-stu-id="efeff-196">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="efeff-197">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="efeff-197">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="efeff-198">JavaScript Embed Sample</span><span class="sxs-lookup"><span data-stu-id="efeff-198">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="efeff-199">More questions?</span><span class="sxs-lookup"><span data-stu-id="efeff-199">More questions?</span></span> [<span data-ttu-id="efeff-200">Try the Power BI Community</span><span class="sxs-lookup"><span data-stu-id="efeff-200">Try the Power BI Community</span></span>](http://community.powerbi.com/)





