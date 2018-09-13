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
# <a name="how-to-send-email-using-sendgrid-from-nodejs"></a>How to Send Email Using SendGrid from Node.js
This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure. The samples are written using the Node.js API. The scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**. For more information on SendGrid and sending email, see the [Next Steps](#next-steps) section.

## <a name="what-is-the-sendgrid-email-service"></a>What is the SendGrid Email Service?
SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy. Common SendGrid usage scenarios include:

* Automatically sending receipts to customers
* Administering distribution lists for sending customers monthly e-fliers and special offers
* Collecting real-time metrics for things like blocked e-mail, and customer responsiveness
* Generating reports to help identify trends
* Forwarding customer inquiries
* Email notifications from your application

For more information, see [https://sendgrid.com](https://sendgrid.com).

## <a name="create-a-sendgrid-account"></a>Create a SendGrid Account
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-the-sendgrid-nodejs-module"></a>Reference the SendGrid Node.js Module
The SendGrid module for Node.js can be installed through the node package manager (npm) by using the following command:

    npm install sendgrid

After installation, you can require the module in your application by using the following code:

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

The SendGrid module exports the **SendGrid** and **Email** functions.
**SendGrid** is responsible for sending email through Web API, while **Email** encapsulates an email message.

## <a name="how-to-create-an-email"></a>How to: Create an Email
Creating an email message using the SendGrid module involves first creating an email message using the Email function, and then sending it using the SendGrid function. The following is an example of creating a new message using the Email function:

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

You can also specify an HTML message for clients that support it by setting the html property. For example:

    html: This is a sample <b>HTML<b> email message.

Setting both the text and html properties provides graceful fallback to text content for clients that cannot support HTML messages.

For more information on all properties supported by the Email function, see [sendgrid-nodejs][sendgrid-nodejs].

## <a name="how-to-send-an-email"></a>How to: Send an Email
After creating an email message using the Email function, you can send it using the Web API provided by SendGrid. 

### <a name="web-api"></a>Web API
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> While the above examples show passing in an email object and callback function, you can also directly invoke the send function by directly specifying email properties. For example:  
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

## <a name="how-to-add-an-attachment"></a>How to: Add an Attachment
Attachments can be added to a message by specifying the file name(s) and path(s) in the **files** property. The following example demonstrates sending an attachment:

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
> When using the **files** property, the file must be accessible through [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile). If the file you wish to attach is hosted in Azure Storage, such as in a Blob container, you must first copy the file to local storage or to an Azure drive before it can be sent as an attachment using the **files** property.
> 
> 

## <a name="how-to-use-filters-to-enable-footers-and-tracking"></a>How to: Use Filters to Enable Footers and Tracking
SendGrid provides additional email functionality through the use of filters. These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on. For a full list of filters, see [Filter Settings][Filter Settings].

Filters can be applied to a message by using the **filters** property.
Each filter is specified by a hash containing filter-specific settings.
The following examples demonstrate the footer and click tracking filters:

### <a name="footer"></a>Footer
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

### <a name="click-tracking"></a>Click Tracking
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

## <a name="how-to-update-email-properties"></a>How to: Update Email Properties
Some email properties can be overwritten using **set*Property*** or appended using **add*Property***. For example, you can add additional recipients by using

    email.addTo('jeff@contoso.com');

or set a filter by using

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

For more information, see [sendgrid-nodejs][sendgrid-nodejs].

## <a name="how-to-use-additional-sendgrid-services"></a>How to: Use Additional SendGrid Services
SendGrid offers web-based APIs that you can use to leverage additional SendGrid functionality from your Azure application. For full details, see the [SendGrid API documentation][SendGrid API documentation].

## <a name="next-steps"></a>Next Steps
Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.

* SendGrid Node.js module repository: [sendgrid-nodejs][sendgrid-nodejs]
* SendGrid API documentation: <https://sendgrid.com/docs>
* SendGrid special offer for Azure customers: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[cloud-based email service]: https://sendgrid.com/email-solutions
[transactional email delivery]: https://sendgrid.com/transactional-email
