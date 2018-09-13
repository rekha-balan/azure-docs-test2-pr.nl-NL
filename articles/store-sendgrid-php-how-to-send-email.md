---
title: How to use the SendGrid email service (PHP) | Microsoft Docs
description: Learn how send email with the SendGrid email service on Azure. Code samples written in PHP.
documentationcenter: php
services: ''
manager: sendgrid
editor: mollybos
author: thinkingserious
ms.assetid: 51a9928a-4c9e-4b0a-aca8-9a408aeb6f47
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork; matt.bernier@sendgrid.com
ms.openlocfilehash: 523b986f66a2e48685e9707903194856f0dcf4a2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555119"
---
# <a name="how-to-use-the-sendgrid-email-service-from-php"></a><span data-ttu-id="67f2d-104">How to Use the SendGrid Email Service from PHP</span><span class="sxs-lookup"><span data-stu-id="67f2d-104">How to Use the SendGrid Email Service from PHP</span></span>
<span data-ttu-id="67f2d-105">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span><span class="sxs-lookup"><span data-stu-id="67f2d-105">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="67f2d-106">The samples are written in PHP.</span><span class="sxs-lookup"><span data-stu-id="67f2d-106">The samples are written in PHP.</span></span>
<span data-ttu-id="67f2d-107">The scenarios covered include **constructing email**, **sending email**, and **adding attachments**.</span><span class="sxs-lookup"><span data-stu-id="67f2d-107">The scenarios covered include **constructing email**, **sending email**, and **adding attachments**.</span></span> <span data-ttu-id="67f2d-108">For more information on SendGrid and sending email, see the [Next Steps](#next-steps) section.</span><span class="sxs-lookup"><span data-stu-id="67f2d-108">For more information on SendGrid and sending email, see the [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="67f2d-109">What is the SendGrid Email Service?</span><span class="sxs-lookup"><span data-stu-id="67f2d-109">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="67f2d-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span><span class="sxs-lookup"><span data-stu-id="67f2d-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="67f2d-111">Common SendGrid usage scenarios include:</span><span class="sxs-lookup"><span data-stu-id="67f2d-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="67f2d-112">Automatically sending receipts to customers</span><span class="sxs-lookup"><span data-stu-id="67f2d-112">Automatically sending receipts to customers</span></span>
* <span data-ttu-id="67f2d-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span><span class="sxs-lookup"><span data-stu-id="67f2d-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="67f2d-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span><span class="sxs-lookup"><span data-stu-id="67f2d-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="67f2d-115">Generating reports to help identify trends</span><span class="sxs-lookup"><span data-stu-id="67f2d-115">Generating reports to help identify trends</span></span>
* <span data-ttu-id="67f2d-116">Forwarding customer inquiries</span><span class="sxs-lookup"><span data-stu-id="67f2d-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="67f2d-117">Email notifications from your application</span><span class="sxs-lookup"><span data-stu-id="67f2d-117">Email notifications from your application</span></span>

<span data-ttu-id="67f2d-118">For more information, see [https://sendgrid.com][https://sendgrid.com].</span><span class="sxs-lookup"><span data-stu-id="67f2d-118">For more information, see [https://sendgrid.com][https://sendgrid.com].</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="67f2d-119">Create a SendGrid Account</span><span class="sxs-lookup"><span data-stu-id="67f2d-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="using-sendgrid-from-your-php-application"></a><span data-ttu-id="67f2d-120">Using SendGrid from your PHP Application</span><span class="sxs-lookup"><span data-stu-id="67f2d-120">Using SendGrid from your PHP Application</span></span>
<span data-ttu-id="67f2d-121">Using SendGrid in an Azure PHP application requires no special configuration or coding.</span><span class="sxs-lookup"><span data-stu-id="67f2d-121">Using SendGrid in an Azure PHP application requires no special configuration or coding.</span></span> <span data-ttu-id="67f2d-122">Because SendGrid is a service, it can be accessed in exactly the same way from a cloud application as it can from an on-premises application.</span><span class="sxs-lookup"><span data-stu-id="67f2d-122">Because SendGrid is a service, it can be accessed in exactly the same way from a cloud application as it can from an on-premises application.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="67f2d-123">How to: Send an Email</span><span class="sxs-lookup"><span data-stu-id="67f2d-123">How to: Send an Email</span></span>
<span data-ttu-id="67f2d-124">You can send email using either SMTP or the Web API provided by SendGrid.</span><span class="sxs-lookup"><span data-stu-id="67f2d-124">You can send email using either SMTP or the Web API provided by SendGrid.</span></span>

### <a name="smtp-api"></a><span data-ttu-id="67f2d-125">SMTP API</span><span class="sxs-lookup"><span data-stu-id="67f2d-125">SMTP API</span></span>
<span data-ttu-id="67f2d-126">To send email using the SendGrid SMTP API, use *Swift Mailer*, a component-based library for sending emails from PHP applications.</span><span class="sxs-lookup"><span data-stu-id="67f2d-126">To send email using the SendGrid SMTP API, use *Swift Mailer*, a component-based library for sending emails from PHP applications.</span></span> <span data-ttu-id="67f2d-127">You can download the *Swift Mailer* library from [http://swiftmailer.org/download][http://swiftmailer.org/download] v5.3.0 (use [Composer] to install Swift Mailer).</span><span class="sxs-lookup"><span data-stu-id="67f2d-127">You can download the *Swift Mailer* library from [http://swiftmailer.org/download][http://swiftmailer.org/download] v5.3.0 (use [Composer] to install Swift Mailer).</span></span> <span data-ttu-id="67f2d-128">Sending email with the library involves creating instances of the <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span>, and <span class="auto-style2">Swift\_Message</span> classes, setting the appropriate properties, and calling the <span class="auto-style2">Swift\_Mailer::send</span> method.</span><span class="sxs-lookup"><span data-stu-id="67f2d-128">Sending email with the library involves creating instances of the <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span>, and <span class="auto-style2">Swift\_Message</span> classes, setting the appropriate properties, and calling the <span class="auto-style2">Swift\_Mailer::send</span> method.</span></span>

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create the body of the message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of the email
      * If the receiver is able to view html emails then only the html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
     $html = "<html>
           <head></head>
           <body>
               <p>Hi!<br>
                   How are you?<br>
               </p>
           </body>
           </html>";
     // This is your From email address
     $from = array('someone@example.com' => 'Name To Appear');
     // Email recipients
     $to = array(
           'john@contoso.com'=>'Destination 1 Name',
           'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach the body of the email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
         // This will let us know how many users received this message
         echo 'Message sent out to '.$recipients.' users';
     }
     // something went wrong =(
     else
     {
         echo "Something went wrong - ";
         print_r($failures);
     }

### <a name="web-api"></a><span data-ttu-id="67f2d-129">Web API</span><span class="sxs-lookup"><span data-stu-id="67f2d-129">Web API</span></span>
<span data-ttu-id="67f2d-130">Use PHP's [curl function][curl function] to send email using the SendGrid Web API.</span><span class="sxs-lookup"><span data-stu-id="67f2d-130">Use PHP's [curl function][curl function] to send email using the SendGrid Web API.</span></span>

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $params = array(
          'api_user' => $user,
          'api_key' => $pass,
          'to' => 'john@contoso.com',
          'subject' => 'testing from curl',
          'html' => 'testing body',
          'text' => 'testing body',
          'from' => 'anna@contoso.com',
       );

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl to use HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is the body of the POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not to return headers, but do return the response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

<span data-ttu-id="67f2d-131">SendGrid's Web API is very similar to a REST API, though it is not truly a RESTful API since, in most calls, both GET and POST verbs can be used interchangeably.</span><span class="sxs-lookup"><span data-stu-id="67f2d-131">SendGrid's Web API is very similar to a REST API, though it is not truly a RESTful API since, in most calls, both GET and POST verbs can be used interchangeably.</span></span>

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="67f2d-132">How to: Add an Attachment</span><span class="sxs-lookup"><span data-stu-id="67f2d-132">How to: Add an Attachment</span></span>
### <a name="smtp-api"></a><span data-ttu-id="67f2d-133">SMTP API</span><span class="sxs-lookup"><span data-stu-id="67f2d-133">SMTP API</span></span>
<span data-ttu-id="67f2d-134">Sending an attachment using the SMTP API involves one additional line of code to the example script for sending an email with Swift Mailer.</span><span class="sxs-lookup"><span data-stu-id="67f2d-134">Sending an attachment using the SMTP API involves one additional line of code to the example script for sending an email with Swift Mailer.</span></span>

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create the body of the message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of the email
      * If the reciever is able to view html emails then only the html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
      $html = "<html>
          <head></head>
          <body>
             <p>Hi!<br>
                How are you?<br>
             </p>
          </body>
          </html>";

     // This is your From email address
     $from = array('someone@example.com' => 'Name To Appear');

     // Email recipients
     $to = array(
          'john@contoso.com'=>'Destination 1 Name',
          'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach the body of the email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');
     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName("file_name"));

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
          // This will let us know how many users received this message
          echo 'Message sent out to '.$recipients.' users';
     }
     // something went wrong =(
     else
     {
          echo "Something went wrong - ";
          print_r($failures);
     }

<span data-ttu-id="67f2d-135">The additional line of code is as follows:</span><span class="sxs-lookup"><span data-stu-id="67f2d-135">The additional line of code is as follows:</span></span>

     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName('file_name'));

<span data-ttu-id="67f2d-136">This line of code calls the attach method on the <span class="auto-style2">Swift\_Message</span> object and uses static method <span class="auto-style2">fromPath</span> on the <span class="auto-style2">Swift\_Attachment</span> class to get and attach a file to a message.</span><span class="sxs-lookup"><span data-stu-id="67f2d-136">This line of code calls the attach method on the <span class="auto-style2">Swift\_Message</span> object and uses static method <span class="auto-style2">fromPath</span> on the <span class="auto-style2">Swift\_Attachment</span> class to get and attach a file to a message.</span></span>

### <a name="web-api"></a><span data-ttu-id="67f2d-137">Web API</span><span class="sxs-lookup"><span data-stu-id="67f2d-137">Web API</span></span>
<span data-ttu-id="67f2d-138">Sending an attachment using the Web API is very similar to sending an email using the Web API.</span><span class="sxs-lookup"><span data-stu-id="67f2d-138">Sending an attachment using the Web API is very similar to sending an email using the Web API.</span></span> <span data-ttu-id="67f2d-139">However, note that in the example that follows, the parameter array must contain this element:</span><span class="sxs-lookup"><span data-stu-id="67f2d-139">However, note that in the example that follows, the parameter array must contain this element:</span></span>

    'files['.$fileName.']' => '@'.$filePath.'/'.$fileName

<span data-ttu-id="67f2d-140">Example:</span><span class="sxs-lookup"><span data-stu-id="67f2d-140">Example:</span></span>

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $fileName = 'myfile';
     $filePath = dirname(__FILE__);

     $params = array(
         'api_user' => $user,
         'api_key' => $pass,
         'to' =>'john@contoso.com',
         'subject' => 'test of file sends',
         'html' => '<p> the HTML </p>',
         'text' => 'the plain text',
         'from' => 'anna@contoso.com',
         'files['.$fileName.']' => '@'.$filePath.'/'.$fileName
     );

     print_r($params);

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl to use HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is the body of the POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not to return headers, but do return the response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

## <a name="how-to-use-filters-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="67f2d-141">How to: Use Filters to Enable Footers, Tracking, and Analytics</span><span class="sxs-lookup"><span data-stu-id="67f2d-141">How to: Use Filters to Enable Footers, Tracking, and Analytics</span></span>
<span data-ttu-id="67f2d-142">SendGrid provides additional email functionality through the use of 'filters'.</span><span class="sxs-lookup"><span data-stu-id="67f2d-142">SendGrid provides additional email functionality through the use of 'filters'.</span></span> <span data-ttu-id="67f2d-143">These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span><span class="sxs-lookup"><span data-stu-id="67f2d-143">These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span>

<span data-ttu-id="67f2d-144">Filters can be applied to a message by using the filters property.</span><span class="sxs-lookup"><span data-stu-id="67f2d-144">Filters can be applied to a message by using the filters property.</span></span> <span data-ttu-id="67f2d-145">Each filter is specified by a hash containing filter-specific settings.</span><span class="sxs-lookup"><span data-stu-id="67f2d-145">Each filter is specified by a hash containing filter-specific settings.</span></span> <span data-ttu-id="67f2d-146">The following example enables the footer filter and specifies a text message that will be appended to the bottom of the email message.</span><span class="sxs-lookup"><span data-stu-id="67f2d-146">The following example enables the footer filter and specifies a text message that will be appended to the bottom of the email message.</span></span>
<span data-ttu-id="67f2d-147">For this example we will use [sendgrid-php library].</span><span class="sxs-lookup"><span data-stu-id="67f2d-147">For this example we will use [sendgrid-php library].</span></span>
<span data-ttu-id="67f2d-148">Use [Composer] to install library:</span><span class="sxs-lookup"><span data-stu-id="67f2d-148">Use [Composer] to install library:</span></span>

    php composer.phar require sendgrid/sendgrid 2.1.1

<span data-ttu-id="67f2d-149">Example:</span><span class="sxs-lookup"><span data-stu-id="67f2d-149">Example:</span></span>    

    <?php
     /*
      * This example is used for sendgrid-php V2.1.1 (https://github.com/sendgrid/sendgrid-php/tree/v2.1.1)
      */
     include "vendor/autoload.php";

     $email = new SendGrid\Email();
     // The list of addresses this message will be sent to
     // [This list is used for sending multiple emails using just ONE request to SendGrid]
     $toList = array('john@contoso.com', 'anna@contoso.com');

     // Specify the names of the recipients
     $nameList = array('Name 1', 'Name 2');

     // Used as an example of variable substitution
     $timeList = array('4 PM', '5 PM');

     // Set all of the above variables
     $email->setTos($toList);
     $email->addSubstitution('-name-', $nameList);
     $email->addSubstitution('-time-', $timeList);

     // Specify that this is an initial contact message
     $email->addCategory("initial");

     // You can optionally setup individual filters here, in this example, we have
     // enabled the footer filter
     $email->addFilter('footer', 'enable', 1);
     $email->addFilter('footer', "text/plain", "Thank you for your business");
     $email->addFilter('footer', "text/html", "Thank you for your business");

     // The subject of your email
     $subject = 'Example SendGrid Email';

     // Where is this message coming from. For example, this message can be from
     // support@yourcompany.com, info@yourcompany.com
     $from = 'someone@example.com';

     // If you do not specify a sender list above, you can specifiy the user here. If
     // a sender list IS specified above, this email address becomes irrelevant.
     $to = 'john@contoso.com';

     # Create the body of the message (a plain-text and an HTML version).
     # text is your plain-text email
     # html is your html version of the email
     # if the receiver is able to view html emails then only the html
     # email will be displayed

     /*
      * Note the variable substitution here =)
      */
     $text = "
     Hello -name-,
     Thank you for your interest in our products. We have set up an appointment to call you at -time- EST to discuss your needs in more detail.
     Regards,
     Fred";

     $html = "
     <html>
     <head></head>
     <body>
     <p>Hello -name-,<br>
     Thank you for your interest in our products. We have set up an appointment
     to call you at -time- EST to discuss your needs in more detail.

     Regards,

     Fred<br>
     </p>
     </body>
     </html>";

     // set subject
     $email->setSubject($subject);

     // attach the body of the email
     $email->setFrom($from);
     $email->setHtml($html);
     $email->addTo($to);
     $email->setText($text);

     // Your SendGrid account credentials
     $username = 'sendgridusername@yourdomain.com';
     $password = 'example';

     // Create SendGrid object
     $sendgrid = new SendGrid($username, $password);

     // send message
     $response = $sendgrid->send($email);

     print_r($response);

## <a name="next-steps"></a><span data-ttu-id="67f2d-150">Next Steps</span><span class="sxs-lookup"><span data-stu-id="67f2d-150">Next Steps</span></span>
<span data-ttu-id="67f2d-151">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span><span class="sxs-lookup"><span data-stu-id="67f2d-151">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="67f2d-152">SendGrid documentation: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="67f2d-152">SendGrid documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="67f2d-153">SendGrid PHP library: <https://github.com/sendgrid/sendgrid-php></span><span class="sxs-lookup"><span data-stu-id="67f2d-153">SendGrid PHP library: <https://github.com/sendgrid/sendgrid-php></span></span>
* <span data-ttu-id="67f2d-154">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="67f2d-154">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

<span data-ttu-id="67f2d-155">For more information, see also the [PHP Developer Center](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="67f2d-155">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[https://sendgrid.com]: https://sendgrid.com
[https://sendgrid.com/transactional-email/pricing]: https://sendgrid.com/transactional-email/pricing
[special offer]: https://www.sendgrid.com/windowsazure.html
[Packaging and Deploying PHP Applications for Azure]: http://msdn.microsoft.com/library/windowsazure/hh674499(v=VS.103).aspx
[http://swiftmailer.org/download]: http://swiftmailer.org/download
[curl function]: http://php.net/curl
[cloud-based email service]: https://sendgrid.com/email-solutions
[transactional email delivery]: https://sendgrid.com/transactional-email
[sendgrid-php library]: https://github.com/sendgrid/sendgrid-php/tree/v2.1.1
[Composer]: https://getcomposer.org/download/
