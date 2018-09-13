---
title: How to use the SendGrid email service (.NET) | Microsoft Docs
description: Learn how send email with the SendGrid email service on Azure. Code samples written in C# and use the .NET API.
services: app-service\web
documentationcenter: .net
author: thinkingserious
manager: erikre
editor: ''
ms.assetid: 21bf4028-9046-476b-9799-3d3082a0f84c
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/15/2017
ms.author: dx@sendgrid.com
ms.openlocfilehash: a5f702cd55c5ea8281caac038a0cd818706e83ad
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563295"
---
# <a name="how-to-send-email-using-sendgrid-with-azure"></a><span data-ttu-id="79c84-104">How to Send Email Using SendGrid with Azure</span><span class="sxs-lookup"><span data-stu-id="79c84-104">How to Send Email Using SendGrid with Azure</span></span>
## <a name="overview"></a><span data-ttu-id="79c84-105">Overview</span><span class="sxs-lookup"><span data-stu-id="79c84-105">Overview</span></span>
<span data-ttu-id="79c84-106">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span><span class="sxs-lookup"><span data-stu-id="79c84-106">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="79c84-107">The samples are written in C\# and supports .NET Standard 1.3.</span><span class="sxs-lookup"><span data-stu-id="79c84-107">The samples are written in C\# and supports .NET Standard 1.3.</span></span> <span data-ttu-id="79c84-108">The scenarios covered include constructing email, sending email, adding attachments, and enabling various mail and tracking settings.</span><span class="sxs-lookup"><span data-stu-id="79c84-108">The scenarios covered include constructing email, sending email, adding attachments, and enabling various mail and tracking settings.</span></span> <span data-ttu-id="79c84-109">For more information on SendGrid and sending email, see the [Next steps][Next steps] section.</span><span class="sxs-lookup"><span data-stu-id="79c84-109">For more information on SendGrid and sending email, see the [Next steps][Next steps] section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="79c84-110">What is the SendGrid Email Service?</span><span class="sxs-lookup"><span data-stu-id="79c84-110">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="79c84-111">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span><span class="sxs-lookup"><span data-stu-id="79c84-111">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="79c84-112">Common SendGrid use cases include:</span><span class="sxs-lookup"><span data-stu-id="79c84-112">Common SendGrid use cases include:</span></span>

* <span data-ttu-id="79c84-113">Automatically sending receipts or purchase confirmations to customers.</span><span class="sxs-lookup"><span data-stu-id="79c84-113">Automatically sending receipts or purchase confirmations to customers.</span></span>
* <span data-ttu-id="79c84-114">Administering distribution lists for sending customers monthly fliers and promotions.</span><span class="sxs-lookup"><span data-stu-id="79c84-114">Administering distribution lists for sending customers monthly fliers and promotions.</span></span>
* <span data-ttu-id="79c84-115">Collecting real-time metrics for things like blocked email and customer engagement.</span><span class="sxs-lookup"><span data-stu-id="79c84-115">Collecting real-time metrics for things like blocked email and customer engagement.</span></span>
* <span data-ttu-id="79c84-116">Forwarding customer inquiries.</span><span class="sxs-lookup"><span data-stu-id="79c84-116">Forwarding customer inquiries.</span></span>
* <span data-ttu-id="79c84-117">Processing incoming emails.</span><span class="sxs-lookup"><span data-stu-id="79c84-117">Processing incoming emails.</span></span>

<span data-ttu-id="79c84-118">For more information, visit [https://sendgrid.com](https://sendgrid.com) or SendGrid's [C# library][sendgrid-csharp] GitHub repo.</span><span class="sxs-lookup"><span data-stu-id="79c84-118">For more information, visit [https://sendgrid.com](https://sendgrid.com) or SendGrid's [C# library][sendgrid-csharp] GitHub repo.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="79c84-119">Create a SendGrid Account</span><span class="sxs-lookup"><span data-stu-id="79c84-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-the-sendgrid-net-class-library"></a><span data-ttu-id="79c84-120">Reference the SendGrid .NET Class Library</span><span class="sxs-lookup"><span data-stu-id="79c84-120">Reference the SendGrid .NET Class Library</span></span>
<span data-ttu-id="79c84-121">The [SendGrid NuGet package](https://www.nuget.org/packages/Sendgrid) is the easiest way to get the SendGrid API and to configure your application with all dependencies.</span><span class="sxs-lookup"><span data-stu-id="79c84-121">The [SendGrid NuGet package](https://www.nuget.org/packages/Sendgrid) is the easiest way to get the SendGrid API and to configure your application with all dependencies.</span></span> <span data-ttu-id="79c84-122">NuGet is a Visual Studio extension included with Microsoft Visual Studio 2015 and above that makes it easy to install and update libraries and tools.</span><span class="sxs-lookup"><span data-stu-id="79c84-122">NuGet is a Visual Studio extension included with Microsoft Visual Studio 2015 and above that makes it easy to install and update libraries and tools.</span></span>

> [!NOTE]
> <span data-ttu-id="79c84-123">To install NuGet if you are running a version of Visual Studio earlier than Visual Studio 2015, visit [http://www.nuget.org](http://www.nuget.org), and click the **Install NuGet** button.</span><span class="sxs-lookup"><span data-stu-id="79c84-123">To install NuGet if you are running a version of Visual Studio earlier than Visual Studio 2015, visit [http://www.nuget.org](http://www.nuget.org), and click the **Install NuGet** button.</span></span>
>
>

<span data-ttu-id="79c84-124">To install the SendGrid NuGet package in your application, do the following:</span><span class="sxs-lookup"><span data-stu-id="79c84-124">To install the SendGrid NuGet package in your application, do the following:</span></span>

1. <span data-ttu-id="79c84-125">Click on **New Project** and select a **Template**.</span><span class="sxs-lookup"><span data-stu-id="79c84-125">Click on **New Project** and select a **Template**.</span></span>

   ![Create a new project][create-new-project]
2. <span data-ttu-id="79c84-127">In **Solution Explorer**, right-click **References**, then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="79c84-127">In **Solution Explorer**, right-click **References**, then click **Manage NuGet Packages**.</span></span>

   ![SendGrid NuGet package][SendGrid-NuGet-package]
3. <span data-ttu-id="79c84-129">Search for **SendGrid** and select the **SendGrid** item in the results list.</span><span class="sxs-lookup"><span data-stu-id="79c84-129">Search for **SendGrid** and select the **SendGrid** item in the results list.</span></span>
4. <span data-ttu-id="79c84-130">Select the latest stable version of the Nuget package from the version dropdown to be able to work with the object model and APIs demonstrated in this article.</span><span class="sxs-lookup"><span data-stu-id="79c84-130">Select the latest stable version of the Nuget package from the version dropdown to be able to work with the object model and APIs demonstrated in this article.</span></span>

   ![SendGrid package][sendgrid-package]
5. <span data-ttu-id="79c84-132">Click **Install** to complete the installation, and then close this dialog.</span><span class="sxs-lookup"><span data-stu-id="79c84-132">Click **Install** to complete the installation, and then close this dialog.</span></span>

<span data-ttu-id="79c84-133">SendGrid's .NET class library is called **SendGrid**.</span><span class="sxs-lookup"><span data-stu-id="79c84-133">SendGrid's .NET class library is called **SendGrid**.</span></span> <span data-ttu-id="79c84-134">It contains the following namespaces:</span><span class="sxs-lookup"><span data-stu-id="79c84-134">It contains the following namespaces:</span></span>

* <span data-ttu-id="79c84-135">**SendGrid** for communicating with SendGrid’s API.</span><span class="sxs-lookup"><span data-stu-id="79c84-135">**SendGrid** for communicating with SendGrid’s API.</span></span>
* <span data-ttu-id="79c84-136">**SendGrid.Helpers.Mail** for helper methods to easily create SendGridMessage objects that specify how to send emails.</span><span class="sxs-lookup"><span data-stu-id="79c84-136">**SendGrid.Helpers.Mail** for helper methods to easily create SendGridMessage objects that specify how to send emails.</span></span>

<span data-ttu-id="79c84-137">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access the SendGrid email service.</span><span class="sxs-lookup"><span data-stu-id="79c84-137">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access the SendGrid email service.</span></span>

    using SendGrid;
    using SendGrid.Helpers.Mail

## <a name="how-to-create-an-email"></a><span data-ttu-id="79c84-138">How to: Create an Email</span><span class="sxs-lookup"><span data-stu-id="79c84-138">How to: Create an Email</span></span>
<span data-ttu-id="79c84-139">Use the **SendGridMessage** object to create an email message.</span><span class="sxs-lookup"><span data-stu-id="79c84-139">Use the **SendGridMessage** object to create an email message.</span></span> <span data-ttu-id="79c84-140">Once the message object is created, you can set properties and methods, including the email sender, the email recipient, and the subject and body of the email.</span><span class="sxs-lookup"><span data-stu-id="79c84-140">Once the message object is created, you can set properties and methods, including the email sender, the email recipient, and the subject and body of the email.</span></span>

<span data-ttu-id="79c84-141">The following example demonstrates how to create a fully populated email object:</span><span class="sxs-lookup"><span data-stu-id="79c84-141">The following example demonstrates how to create a fully populated email object:</span></span>

    var msg = new SendGridMessage();

    msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

    var recipients = new List<EmailAddress>
    {
        new EmailAddress("jeff@example.com", "Jeff Smith"),
        new EmailAddress("anna@example.com", "Anna Lidman"),
        new EmailAddress("peter@example.com", "Peter Saddow")
    };
    msg.AddTos(recipients);

    msg.SetSubject("Testing the SendGrid C# Library");

    msg.AddContent(MimeType.Text, "Hello World plain text!");
    msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

<span data-ttu-id="79c84-142">For more information on all properties and methods supported by the **SendGrid** type, see [sendgrid-csharp][sendgrid-csharp] on GitHub.</span><span class="sxs-lookup"><span data-stu-id="79c84-142">For more information on all properties and methods supported by the **SendGrid** type, see [sendgrid-csharp][sendgrid-csharp] on GitHub.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="79c84-143">How to: Send an Email</span><span class="sxs-lookup"><span data-stu-id="79c84-143">How to: Send an Email</span></span>
<span data-ttu-id="79c84-144">After creating an email message, you can send it using SendGrid's API.</span><span class="sxs-lookup"><span data-stu-id="79c84-144">After creating an email message, you can send it using SendGrid's API.</span></span> <span data-ttu-id="79c84-145">Alternatively, you may use [.NET's built in library][NET-library].</span><span class="sxs-lookup"><span data-stu-id="79c84-145">Alternatively, you may use [.NET's built in library][NET-library].</span></span>

<span data-ttu-id="79c84-146">Sending email requires that you supply your SendGrid API Key.</span><span class="sxs-lookup"><span data-stu-id="79c84-146">Sending email requires that you supply your SendGrid API Key.</span></span> <span data-ttu-id="79c84-147">If you need details about how to configure API Keys, please visit SendGrid's API Keys [documentation][documentation].</span><span class="sxs-lookup"><span data-stu-id="79c84-147">If you need details about how to configure API Keys, please visit SendGrid's API Keys [documentation][documentation].</span></span>

<span data-ttu-id="79c84-148">You may store these credentials via your Azure Portal by clicking Application settings and adding the key/value pairs under App settings.</span><span class="sxs-lookup"><span data-stu-id="79c84-148">You may store these credentials via your Azure Portal by clicking Application settings and adding the key/value pairs under App settings.</span></span>

 ![Azure app settings][azure_app_settings]

 <span data-ttu-id="79c84-150">Then, you may access them as follows:</span><span class="sxs-lookup"><span data-stu-id="79c84-150">Then, you may access them as follows:</span></span>

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

<span data-ttu-id="79c84-151">The following examples show how to send a message using the Web API.</span><span class="sxs-lookup"><span data-stu-id="79c84-151">The following examples show how to send a message using the Web API.</span></span>

    using System;
    using System.Threading.Tasks;
    using SendGrid;
    using SendGrid.Helpers.Mail;

    namespace Example
    {
        internal class Example
        {
            private static void Main()
            {
                Execute().Wait();
            }

            static async Task Execute()
            {
                var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
                var client = new SendGridClient(apiKey);
                var msg = new SendGridMessage()
                {
                    From = new EmailAddress("test@example.com", "DX Team"),
                    Subject = "Hello World from the SendGrid CSharp SDK!",
                    PlainTextContent = "Hello, Email!",
                    HtmlContent = "<strong>Hello, Email!</strong>"
                };
                msg.AddTo(new EmailAddress("test@example.com", "Test User"));
                var response = await client.SendEmailAsync(msg);
            }
        }
    }

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="79c84-152">How to: Add an attachment</span><span class="sxs-lookup"><span data-stu-id="79c84-152">How to: Add an attachment</span></span>
<span data-ttu-id="79c84-153">Attachments can be added to a message by calling the **AddAttachment** method and minimally specifying the file name and Base64 encoded content you want to attach.</span><span class="sxs-lookup"><span data-stu-id="79c84-153">Attachments can be added to a message by calling the **AddAttachment** method and minimally specifying the file name and Base64 encoded content you want to attach.</span></span> <span data-ttu-id="79c84-154">You can include multiple attachments by calling this method once for each file you wish to attach or by using the **AddAttachments** method.</span><span class="sxs-lookup"><span data-stu-id="79c84-154">You can include multiple attachments by calling this method once for each file you wish to attach or by using the **AddAttachments** method.</span></span> <span data-ttu-id="79c84-155">The following example demonstrates adding an attachment to a message:</span><span class="sxs-lookup"><span data-stu-id="79c84-155">The following example demonstrates adding an attachment to a message:</span></span>

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="79c84-156">How to: Use mail settings to enable footers, tracking, and analytics</span><span class="sxs-lookup"><span data-stu-id="79c84-156">How to: Use mail settings to enable footers, tracking, and analytics</span></span>
<span data-ttu-id="79c84-157">SendGrid provides additional email functionality through the use of mail settings and tracking settings.</span><span class="sxs-lookup"><span data-stu-id="79c84-157">SendGrid provides additional email functionality through the use of mail settings and tracking settings.</span></span> <span data-ttu-id="79c84-158">These settings can be added to an email message to enable specific functionality such as click tracking, Google analytics, subscription tracking, and so on.</span><span class="sxs-lookup"><span data-stu-id="79c84-158">These settings can be added to an email message to enable specific functionality such as click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="79c84-159">For a full list of apps, see the [Settings Documentation][settings-documentation].</span><span class="sxs-lookup"><span data-stu-id="79c84-159">For a full list of apps, see the [Settings Documentation][settings-documentation].</span></span>

<span data-ttu-id="79c84-160">Apps can be applied to **SendGrid** email messages using methods implemented as part of the **SendGridMessage** class.</span><span class="sxs-lookup"><span data-stu-id="79c84-160">Apps can be applied to **SendGrid** email messages using methods implemented as part of the **SendGridMessage** class.</span></span> <span data-ttu-id="79c84-161">The following examples demonstrate the footer and click tracking filters:</span><span class="sxs-lookup"><span data-stu-id="79c84-161">The following examples demonstrate the footer and click tracking filters:</span></span>

<span data-ttu-id="79c84-162">The following examples demonstrate the footer and click tracking filters:</span><span class="sxs-lookup"><span data-stu-id="79c84-162">The following examples demonstrate the footer and click tracking filters:</span></span>

### <a name="footer-settings"></a><span data-ttu-id="79c84-163">Footer settings</span><span class="sxs-lookup"><span data-stu-id="79c84-163">Footer settings</span></span>
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a><span data-ttu-id="79c84-164">Click tracking</span><span class="sxs-lookup"><span data-stu-id="79c84-164">Click tracking</span></span>
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="79c84-165">How to: Use Additional SendGrid Services</span><span class="sxs-lookup"><span data-stu-id="79c84-165">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="79c84-166">SendGrid offers several APIs and webhooks that you can use to leverage additional functionality within your Azure application.</span><span class="sxs-lookup"><span data-stu-id="79c84-166">SendGrid offers several APIs and webhooks that you can use to leverage additional functionality within your Azure application.</span></span> <span data-ttu-id="79c84-167">For more details, see the [SendGrid API Reference][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="79c84-167">For more details, see the [SendGrid API Reference][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="79c84-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="79c84-168">Next steps</span></span>
<span data-ttu-id="79c84-169">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span><span class="sxs-lookup"><span data-stu-id="79c84-169">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="79c84-170">SendGrid C\# library repo: [sendgrid-csharp][sendgrid-csharp]</span><span class="sxs-lookup"><span data-stu-id="79c84-170">SendGrid C\# library repo: [sendgrid-csharp][sendgrid-csharp]</span></span>
* <span data-ttu-id="79c84-171">SendGrid API documentation: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="79c84-171">SendGrid API documentation: <https://sendgrid.com/docs></span></span>

[Next steps]: #next-steps
[What is the SendGrid Email Service?]: #whatis
[Create a SendGrid Account]: #createaccount
[Reference the SendGrid .NET Class Library]: #reference
[How to: Create an Email]: #createemail
[How to: Send an Email]: #sendemail
[How to: Add an Attachment]: #addattachment
[How to: Use Filters to Enable Footers, Tracking, and Analytics]: #usefilters
[How to: Use Additional SendGrid Services]: #useservices

[create-new-project]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/sendgrid-dotnet-how-to-send-email/new-project.png
[SendGrid-NuGet-package]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/sendgrid-dotnet-how-to-send-email/reference.png
[sendgrid-package]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/sendgrid-dotnet-how-to-send-email/sendgrid-package.png
[azure_app_settings]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/sendgrid-dotnet-how-to-send-email/azure-app-settings.png
[sendgrid-csharp]: https://github.com/sendgrid/sendgrid-csharp
[SMTP vs. Web API]: https://sendgrid.com/docs/Integrate/index.html
[App Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/api_v3.html
[NET-library]: https://sendgrid.com/docs/Integrate/Code_Examples/v2_Mail/csharp.html#-Using-NETs-Builtin-SMTP-Library
[documentation]: https://sendgrid.com/docs/Classroom/Send/api_keys.html
[settings-documentation]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html

[cloud-based email service]: https://sendgrid.com/solutions
[transactional email delivery]: https://sendgrid.com/use-cases/transactional-email





