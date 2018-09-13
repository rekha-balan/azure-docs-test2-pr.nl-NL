---
title: How to use the SendGrid email service (Node.js) | Microsoft Docs
description: Learn how send email with the SendGrid email service on Azure. Code samples written using the Node.js API.
services: ''
documentationcenter: nodejs
author: erikre
manager: wpickett
editor: ''
ms.assetid: cac444b4-26b0-45ea-9c3d-eca28d57dacb
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 01/05/2016
ms.author: erikre
ms.openlocfilehash: 327cea3a24cc47a9cc463b37cc2346ebc475ef7f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662883"
---
# <a name="how-to-send-email-using-sendgrid-from-nodejs"></a><span data-ttu-id="2f1db-104">How to Send Email Using SendGrid from Node.js</span><span class="sxs-lookup"><span data-stu-id="2f1db-104">How to Send Email Using SendGrid from Node.js</span></span>
<span data-ttu-id="2f1db-105">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span><span class="sxs-lookup"><span data-stu-id="2f1db-105">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="2f1db-106">The samples are written using the Node.js API.</span><span class="sxs-lookup"><span data-stu-id="2f1db-106">The samples are written using the Node.js API.</span></span> <span data-ttu-id="2f1db-107">The scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span><span class="sxs-lookup"><span data-stu-id="2f1db-107">The scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="2f1db-108">For more information on SendGrid and sending email, see the [Next Steps](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="2f1db-108">For more information on SendGrid and sending email, see the [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="2f1db-109">What is the SendGrid Email Service?</span><span class="sxs-lookup"><span data-stu-id="2f1db-109">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="2f1db-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span><span class="sxs-lookup"><span data-stu-id="2f1db-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="2f1db-111">Common SendGrid usage scenarios include:</span><span class="sxs-lookup"><span data-stu-id="2f1db-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="2f1db-112">Automatically sending receipts to customers</span><span class="sxs-lookup"><span data-stu-id="2f1db-112">Automatically sending receipts to customers</span></span>
* <span data-ttu-id="2f1db-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span><span class="sxs-lookup"><span data-stu-id="2f1db-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="2f1db-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span><span class="sxs-lookup"><span data-stu-id="2f1db-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="2f1db-115">Generating reports to help identify trends</span><span class="sxs-lookup"><span data-stu-id="2f1db-115">Generating reports to help identify trends</span></span>
* <span data-ttu-id="2f1db-116">Forwarding customer inquiries</span><span class="sxs-lookup"><span data-stu-id="2f1db-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="2f1db-117">Email notifications from your application</span><span class="sxs-lookup"><span data-stu-id="2f1db-117">Email notifications from your application</span></span>

<span data-ttu-id="2f1db-118">For more information, see [https://sendgrid.com](https://sendgrid.com).</span><span class="sxs-lookup"><span data-stu-id="2f1db-118">For more information, see [https://sendgrid.com](https://sendgrid.com).</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="2f1db-119">Create a SendGrid Account</span><span class="sxs-lookup"><span data-stu-id="2f1db-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-the-sendgrid-nodejs-module"></a><span data-ttu-id="2f1db-120">Reference the SendGrid Node.js Module</span><span class="sxs-lookup"><span data-stu-id="2f1db-120">Reference the SendGrid Node.js Module</span></span>
<span data-ttu-id="2f1db-121">The SendGrid module for Node.js can be installed through the node package manager (npm) by using the following command:</span><span class="sxs-lookup"><span data-stu-id="2f1db-121">The SendGrid module for Node.js can be installed through the node package manager (npm) by using the following command:</span></span>

    npm install sendgrid

<span data-ttu-id="2f1db-122">After installation, you can require the module in your application by using the following code:</span><span class="sxs-lookup"><span data-stu-id="2f1db-122">After installation, you can require the module in your application by using the following code:</span></span>

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

<span data-ttu-id="2f1db-123">The SendGrid module exports the **SendGrid** and **Email** functions.</span><span class="sxs-lookup"><span data-stu-id="2f1db-123">The SendGrid module exports the **SendGrid** and **Email** functions.</span></span>
<span data-ttu-id="2f1db-124">**SendGrid** is responsible for sending email through Web API, while **Email** encapsulates an email message.</span><span class="sxs-lookup"><span data-stu-id="2f1db-124">**SendGrid** is responsible for sending email through Web API, while **Email** encapsulates an email message.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="2f1db-125">How to: Create an Email</span><span class="sxs-lookup"><span data-stu-id="2f1db-125">How to: Create an Email</span></span>
<span data-ttu-id="2f1db-126">Creating an email message using the SendGrid module involves first creating an email message using the Email function, and then sending it using the SendGrid function.</span><span class="sxs-lookup"><span data-stu-id="2f1db-126">Creating an email message using the SendGrid module involves first creating an email message using the Email function, and then sending it using the SendGrid function.</span></span> <span data-ttu-id="2f1db-127">The following is an example of creating a new message using the Email function:</span><span class="sxs-lookup"><span data-stu-id="2f1db-127">The following is an example of creating a new message using the Email function:</span></span>

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

<span data-ttu-id="2f1db-128">You can also specify an HTML message for clients that support it by setting the html property.</span><span class="sxs-lookup"><span data-stu-id="2f1db-128">You can also specify an HTML message for clients that support it by setting the html property.</span></span> <span data-ttu-id="2f1db-129">For example:</span><span class="sxs-lookup"><span data-stu-id="2f1db-129">For example:</span></span>

    html: This is a sample <b>HTML<b> email message.

<span data-ttu-id="2f1db-130">Setting both the text and html properties provides graceful fallback to text content for clients that cannot support HTML messages.</span><span class="sxs-lookup"><span data-stu-id="2f1db-130">Setting both the text and html properties provides graceful fallback to text content for clients that cannot support HTML messages.</span></span>

<span data-ttu-id="2f1db-131">For more information on all properties supported by the Email function, see [sendgrid-nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="2f1db-131">For more information on all properties supported by the Email function, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="2f1db-132">How to: Send an Email</span><span class="sxs-lookup"><span data-stu-id="2f1db-132">How to: Send an Email</span></span>
<span data-ttu-id="2f1db-133">After creating an email message using the Email function, you can send it using the Web API provided by SendGrid.</span><span class="sxs-lookup"><span data-stu-id="2f1db-133">After creating an email message using the Email function, you can send it using the Web API provided by SendGrid.</span></span> 

### <a name="web-api"></a><span data-ttu-id="2f1db-134">Web API</span><span class="sxs-lookup"><span data-stu-id="2f1db-134">Web API</span></span>
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> <span data-ttu-id="2f1db-135">While the above examples show passing in an email object and callback function, you can also directly invoke the send function by directly specifying email properties.</span><span class="sxs-lookup"><span data-stu-id="2f1db-135">While the above examples show passing in an email object and callback function, you can also directly invoke the send function by directly specifying email properties.</span></span> <span data-ttu-id="2f1db-136">For example:</span><span class="sxs-lookup"><span data-stu-id="2f1db-136">For example:</span></span>  
> 
> `````
> sendgrid.send({
> to: 'john@contoso.com',
> from: 'anna@contoso.com',
> subject: 'test mail',
> text: 'This is a sample email message.'
> });
> `````
> 
> 

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="2f1db-137">How to: Add an Attachment</span><span class="sxs-lookup"><span data-stu-id="2f1db-137">How to: Add an Attachment</span></span>
<span data-ttu-id="2f1db-138">Attachments can be added to a message by specifying the file name(s) and path(s) in the **files** property.</span><span class="sxs-lookup"><span data-stu-id="2f1db-138">Attachments can be added to a message by specifying the file name(s) and path(s) in the **files** property.</span></span> <span data-ttu-id="2f1db-139">The following example demonstrates sending an attachment:</span><span class="sxs-lookup"><span data-stu-id="2f1db-139">The following example demonstrates sending an attachment:</span></span>

    sendgrid.send({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.',
        files: [
            {
                filename:     '',           // required only if file.content is used.
                contentType:  '',           // optional
                cid:          '',           // optional, used to specify cid for inline content
                path:         '',           //
                url:          '',           // == One of these three options is required
                content:      ('' | Buffer) //
            }
        ],
    });

> [!NOTE]
> <span data-ttu-id="2f1db-140">When using the **files** property, the file must be accessible through [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span><span class="sxs-lookup"><span data-stu-id="2f1db-140">When using the **files** property, the file must be accessible through [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span></span> <span data-ttu-id="2f1db-141">If the file you wish to attach is hosted in Azure Storage, such as in a Blob container, you must first copy the file to local storage or to an Azure drive before it can be sent as an attachment using the **files** property.</span><span class="sxs-lookup"><span data-stu-id="2f1db-141">If the file you wish to attach is hosted in Azure Storage, such as in a Blob container, you must first copy the file to local storage or to an Azure drive before it can be sent as an attachment using the **files** property.</span></span>
> 
> 

## <a name="how-to-use-filters-to-enable-footers-and-tracking"></a><span data-ttu-id="2f1db-142">How to: Use Filters to Enable Footers and Tracking</span><span class="sxs-lookup"><span data-stu-id="2f1db-142">How to: Use Filters to Enable Footers and Tracking</span></span>
<span data-ttu-id="2f1db-143">SendGrid provides additional email functionality through the use of filters.</span><span class="sxs-lookup"><span data-stu-id="2f1db-143">SendGrid provides additional email functionality through the use of filters.</span></span> <span data-ttu-id="2f1db-144">These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span><span class="sxs-lookup"><span data-stu-id="2f1db-144">These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="2f1db-145">For a full list of filters, see [Filter Settings][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="2f1db-145">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

<span data-ttu-id="2f1db-146">Filters can be applied to a message by using the **filters** property.</span><span class="sxs-lookup"><span data-stu-id="2f1db-146">Filters can be applied to a message by using the **filters** property.</span></span>
<span data-ttu-id="2f1db-147">Each filter is specified by a hash containing filter-specific settings.</span><span class="sxs-lookup"><span data-stu-id="2f1db-147">Each filter is specified by a hash containing filter-specific settings.</span></span>
<span data-ttu-id="2f1db-148">The following examples demonstrate the footer and click tracking filters:</span><span class="sxs-lookup"><span data-stu-id="2f1db-148">The following examples demonstrate the footer and click tracking filters:</span></span>

### <a name="footer"></a><span data-ttu-id="2f1db-149">Footer</span><span class="sxs-lookup"><span data-stu-id="2f1db-149">Footer</span></span>
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'footer': {
            'settings': {
                'enable': 1,
                'text/plain': 'This is a text footer.'
            }
        }
    });

    sendgrid.send(email);

### <a name="click-tracking"></a><span data-ttu-id="2f1db-150">Click Tracking</span><span class="sxs-lookup"><span data-stu-id="2f1db-150">Click Tracking</span></span>
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'clicktrack': {
            'settings': {
                'enable': 1
            }
        }
    });

    sendgrid.send(email);

## <a name="how-to-update-email-properties"></a><span data-ttu-id="2f1db-151">How to: Update Email Properties</span><span class="sxs-lookup"><span data-stu-id="2f1db-151">How to: Update Email Properties</span></span>
<span data-ttu-id="2f1db-152">Some email properties can be overwritten using **set\*Property**\* or appended using \**add*Property\*\*\*.</span><span class="sxs-lookup"><span data-stu-id="2f1db-152">Some email properties can be overwritten using **set\*Property**\* or appended using \**add*Property\*\*\*.</span></span> <span data-ttu-id="2f1db-153">For example, you can add additional recipients by using</span><span class="sxs-lookup"><span data-stu-id="2f1db-153">For example, you can add additional recipients by using</span></span>

    email.addTo('jeff@contoso.com');

<span data-ttu-id="2f1db-154">or set a filter by using</span><span class="sxs-lookup"><span data-stu-id="2f1db-154">or set a filter by using</span></span>

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

<span data-ttu-id="2f1db-155">For more information, see [sendgrid-nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="2f1db-155">For more information, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="2f1db-156">How to: Use Additional SendGrid Services</span><span class="sxs-lookup"><span data-stu-id="2f1db-156">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="2f1db-157">SendGrid offers web-based APIs that you can use to leverage additional SendGrid functionality from your Azure application.</span><span class="sxs-lookup"><span data-stu-id="2f1db-157">SendGrid offers web-based APIs that you can use to leverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="2f1db-158">For full details, see the [SendGrid API documentation][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="2f1db-158">For full details, see the [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f1db-159">Next Steps</span><span class="sxs-lookup"><span data-stu-id="2f1db-159">Next Steps</span></span>
<span data-ttu-id="2f1db-160">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span><span class="sxs-lookup"><span data-stu-id="2f1db-160">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="2f1db-161">SendGrid Node.js module repository: [sendgrid-nodejs][sendgrid-nodejs]</span><span class="sxs-lookup"><span data-stu-id="2f1db-161">SendGrid Node.js module repository: [sendgrid-nodejs][sendgrid-nodejs]</span></span>
* <span data-ttu-id="2f1db-162">SendGrid API documentation: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="2f1db-162">SendGrid API documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="2f1db-163">SendGrid special offer for Azure customers: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span><span class="sxs-lookup"><span data-stu-id="2f1db-163">SendGrid special offer for Azure customers: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span></span>

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[cloud-based email service]: https://sendgrid.com/email-solutions
[transactional email delivery]: https://sendgrid.com/transactional-email
