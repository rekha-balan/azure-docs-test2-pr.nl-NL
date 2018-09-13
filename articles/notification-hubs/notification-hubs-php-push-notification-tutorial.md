---
title: How to use Notification Hubs with PHP
description: Learn how to use Azure Notification Hubs from a PHP back-end.
services: notification-hubs
documentationcenter: ''
author: dimazaid
manager: kpiteira
editor: spelluru
ms.assetid: 0156f994-96d0-4878-b07b-49b7be4fd856
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: php
ms.devlang: php
ms.topic: article
ms.date: 04/14/2018
ms.author: dimazaid
ms.openlocfilehash: b812d60363ffebf1f4374b6fd44dff5e67497e08
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44810445"
---
# <a name="how-to-use-notification-hubs-from-php"></a><span data-ttu-id="03558-103">How to use Notification Hubs from PHP</span><span class="sxs-lookup"><span data-stu-id="03558-103">How to use Notification Hubs from PHP</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="03558-104">You can access all Notification Hubs features from a Java/PHP/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="03558-104">You can access all Notification Hubs features from a Java/PHP/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

<span data-ttu-id="03558-105">In this topic we show how to:</span><span class="sxs-lookup"><span data-stu-id="03558-105">In this topic we show how to:</span></span>

* <span data-ttu-id="03558-106">Build a REST client for Notification Hubs features in PHP;</span><span class="sxs-lookup"><span data-stu-id="03558-106">Build a REST client for Notification Hubs features in PHP;</span></span>
* <span data-ttu-id="03558-107">Follow the [Get started tutorial](notification-hubs-ios-apple-push-notification-apns-get-started.md) for your mobile platform of choice, implementing the back-end portion in PHP.</span><span class="sxs-lookup"><span data-stu-id="03558-107">Follow the [Get started tutorial](notification-hubs-ios-apple-push-notification-apns-get-started.md) for your mobile platform of choice, implementing the back-end portion in PHP.</span></span>

## <a name="client-interface"></a><span data-ttu-id="03558-108">Client interface</span><span class="sxs-lookup"><span data-stu-id="03558-108">Client interface</span></span>
<span data-ttu-id="03558-109">The main client interface can provide the same methods that are available in the [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), which allows you to directly translate all the tutorials and samples currently available on this site, and contributed by the community on the internet.</span><span class="sxs-lookup"><span data-stu-id="03558-109">The main client interface can provide the same methods that are available in the [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), which allows you to directly translate all the tutorials and samples currently available on this site, and contributed by the community on the internet.</span></span>

<span data-ttu-id="03558-110">You can find all the code available in the [PHP REST wrapper sample].</span><span class="sxs-lookup"><span data-stu-id="03558-110">You can find all the code available in the [PHP REST wrapper sample].</span></span>

<span data-ttu-id="03558-111">For example, to create a client:</span><span class="sxs-lookup"><span data-stu-id="03558-111">For example, to create a client:</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="03558-112">To send an iOS native notification:</span><span class="sxs-lookup"><span data-stu-id="03558-112">To send an iOS native notification:</span></span>

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a><span data-ttu-id="03558-113">Implementation</span><span class="sxs-lookup"><span data-stu-id="03558-113">Implementation</span></span>
<span data-ttu-id="03558-114">If you did not already, follow the [Get started tutorial] up to the last section where you have to implement the back-end.</span><span class="sxs-lookup"><span data-stu-id="03558-114">If you did not already, follow the [Get started tutorial] up to the last section where you have to implement the back-end.</span></span>
<span data-ttu-id="03558-115">Also, if you want you can use the code from the [PHP REST wrapper sample] and go directly to the [Complete the tutorial](#complete-tutorial) section.</span><span class="sxs-lookup"><span data-stu-id="03558-115">Also, if you want you can use the code from the [PHP REST wrapper sample] and go directly to the [Complete the tutorial](#complete-tutorial) section.</span></span>

<span data-ttu-id="03558-116">All the details to implement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="03558-116">All the details to implement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="03558-117">In this section, we describe the PHP implementation of the main steps required to access Notification Hubs REST endpoints:</span><span class="sxs-lookup"><span data-stu-id="03558-117">In this section, we describe the PHP implementation of the main steps required to access Notification Hubs REST endpoints:</span></span>

1. <span data-ttu-id="03558-118">Parse the connection string</span><span class="sxs-lookup"><span data-stu-id="03558-118">Parse the connection string</span></span>
2. <span data-ttu-id="03558-119">Generate the authorization token</span><span class="sxs-lookup"><span data-stu-id="03558-119">Generate the authorization token</span></span>
3. <span data-ttu-id="03558-120">Perform the HTTP call</span><span class="sxs-lookup"><span data-stu-id="03558-120">Perform the HTTP call</span></span>

### <a name="parse-the-connection-string"></a><span data-ttu-id="03558-121">Parse the connection string</span><span class="sxs-lookup"><span data-stu-id="03558-121">Parse the connection string</span></span>
<span data-ttu-id="03558-122">Here is the main class implementing the client, whose constructor that parses the connection string:</span><span class="sxs-lookup"><span data-stu-id="03558-122">Here is the main class implementing the client, whose constructor that parses the connection string:</span></span>

    class NotificationHub {
        const API_VERSION = "?api-version=2013-10";

        private $endpoint;
        private $hubPath;
        private $sasKeyName;
        private $sasKeyValue;

        function __construct($connectionString, $hubPath) {
            $this->hubPath = $hubPath;

            $this->parseConnectionString($connectionString);
        }

        private function parseConnectionString($connectionString) {
            $parts = explode(";", $connectionString);
            if (sizeof($parts) != 3) {
                throw new Exception("Error parsing connection string: " . $connectionString);
            }

            foreach ($parts as $part) {
                if (strpos($part, "Endpoint") === 0) {
                    $this->endpoint = "https" . substr($part, 11);
                } else if (strpos($part, "SharedAccessKeyName") === 0) {
                    $this->sasKeyName = substr($part, 20);
                } else if (strpos($part, "SharedAccessKey") === 0) {
                    $this->sasKeyValue = substr($part, 16);
                }
            }
        }
    }


### <a name="create-security-token"></a><span data-ttu-id="03558-123">Create security token</span><span class="sxs-lookup"><span data-stu-id="03558-123">Create security token</span></span>
<span data-ttu-id="03558-124">The details of the security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="03558-124">The details of the security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="03558-125">The following method has to be added to the **NotificationHub** class to create the token based on the URI of the current request and the credentials extracted from the connection string.</span><span class="sxs-lookup"><span data-stu-id="03558-125">The following method has to be added to the **NotificationHub** class to create the token based on the URI of the current request and the credentials extracted from the connection string.</span></span>

    private function generateSasToken($uri) {
        $targetUri = strtolower(rawurlencode(strtolower($uri)));

        $expires = time();
        $expiresInMins = 60;
        $expires = $expires + $expiresInMins * 60;
        $toSign = $targetUri . "\n" . $expires;

        $signature = rawurlencode(base64_encode(hash_hmac('sha256', $toSign, $this->sasKeyValue, TRUE)));

        $token = "SharedAccessSignature sr=" . $targetUri . "&sig="
                    . $signature . "&se=" . $expires . "&skn=" . $this->sasKeyName;

        return $token;
    }

### <a name="send-a-notification"></a><span data-ttu-id="03558-126">Send a notification</span><span class="sxs-lookup"><span data-stu-id="03558-126">Send a notification</span></span>
<span data-ttu-id="03558-127">First, let us define a class representing a notification.</span><span class="sxs-lookup"><span data-stu-id="03558-127">First, let us define a class representing a notification.</span></span>

    class Notification {
        public $format;
        public $payload;

        # array with keynames for headers
        # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
        # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
        public $headers;

        function __construct($format, $payload) {
            if (!in_array($format, ["template", "apple", "windows", "gcm", "windowsphone"])) {
                throw new Exception('Invalid format: ' . $format);
            }

            $this->format = $format;
            $this->payload = $payload;
        }
    }

<span data-ttu-id="03558-128">This class is a container for a native notification body, or a set of properties on case of a template notification, and a set of headers, which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span><span class="sxs-lookup"><span data-stu-id="03558-128">This class is a container for a native notification body, or a set of properties on case of a template notification, and a set of headers, which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="03558-129">Refer to the [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and the specific notification platforms' formats for all the options available.</span><span class="sxs-lookup"><span data-stu-id="03558-129">Refer to the [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and the specific notification platforms' formats for all the options available.</span></span>

<span data-ttu-id="03558-130">Armed with this class, we can now write the send notification methods inside of the **NotificationHub** class.</span><span class="sxs-lookup"><span data-stu-id="03558-130">Armed with this class, we can now write the send notification methods inside of the **NotificationHub** class.</span></span>

    public function sendNotification($notification, $tagsOrTagExpression="") {
        if (is_array($tagsOrTagExpression)) {
            $tagExpression = implode(" || ", $tagsOrTagExpression);
        } else {
            $tagExpression = $tagsOrTagExpression;
        }

        # build uri
        $uri = $this->endpoint . $this->hubPath . "/messages" . NotificationHub::API_VERSION;
        $ch = curl_init($uri);

        if (in_array($notification->format, ["template", "apple", "gcm"])) {
            $contentType = "application/json";
        } else {
            $contentType = "application/xml";
        }

        $token = $this->generateSasToken($uri);

        $headers = [
            'Authorization: '.$token,
            'Content-Type: '.$contentType,
            'ServiceBusNotification-Format: '.$notification->format
        ];

        if ("" !== $tagExpression) {
            $headers[] = 'ServiceBusNotification-Tags: '.$tagExpression;
        }

        # add headers for other platforms
        if (is_array($notification->headers)) {
            $headers = array_merge($headers, $notification->headers);
        }

        curl_setopt_array($ch, array(
            CURLOPT_POST => TRUE,
            CURLOPT_RETURNTRANSFER => TRUE,
            CURLOPT_SSL_VERIFYPEER => FALSE,
            CURLOPT_HTTPHEADER => $headers,
            CURLOPT_POSTFIELDS => $notification->payload
        ));

        // Send the request
        $response = curl_exec($ch);

        // Check for errors
        if($response === FALSE){
            throw new Exception(curl_error($ch));
        }

        $info = curl_getinfo($ch);

        if ($info['http_code'] <> 201) {
            throw new Exception('Error sending notificaiton: '. $info['http_code'] . ' msg: ' . $response);
        }
    } 

<span data-ttu-id="03558-131">The above methods send an HTTP POST request to the /messages endpoint of your notification hub, with the correct body and headers to send the notification.</span><span class="sxs-lookup"><span data-stu-id="03558-131">The above methods send an HTTP POST request to the /messages endpoint of your notification hub, with the correct body and headers to send the notification.</span></span>

## <a name="complete-tutorial"></a><span data-ttu-id="03558-132">Complete the tutorial</span><span class="sxs-lookup"><span data-stu-id="03558-132">Complete the tutorial</span></span>
<span data-ttu-id="03558-133">Now you can complete the Get Started tutorial by sending the notification from a PHP back-end.</span><span class="sxs-lookup"><span data-stu-id="03558-133">Now you can complete the Get Started tutorial by sending the notification from a PHP back-end.</span></span>

<span data-ttu-id="03558-134">Initialize your Notification Hubs client (substitute the connection string and hub name as instructed in the [Get started tutorial]):</span><span class="sxs-lookup"><span data-stu-id="03558-134">Initialize your Notification Hubs client (substitute the connection string and hub name as instructed in the [Get started tutorial]):</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="03558-135">Then add the send code depending on your target mobile platform.</span><span class="sxs-lookup"><span data-stu-id="03558-135">Then add the send code depending on your target mobile platform.</span></span>

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="03558-136">Windows Store and Windows Phone 8.1 (non-Silverlight)</span><span class="sxs-lookup"><span data-stu-id="03558-136">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a><span data-ttu-id="03558-137">iOS</span><span class="sxs-lookup"><span data-stu-id="03558-137">iOS</span></span>
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a><span data-ttu-id="03558-138">Android</span><span class="sxs-lookup"><span data-stu-id="03558-138">Android</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="03558-139">Windows Phone 8.0 and 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="03558-139">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    $toast = '<?xml version="1.0" encoding="utf-8"?>' .
                '<wp:Notification xmlns:wp="WPNotification">' .
                   '<wp:Toast>' .
                        '<wp:Text1>Hello from PHP!</wp:Text1>' .
                   '</wp:Toast> ' .
                '</wp:Notification>';
    $notification = new Notification("windowsphone", $toast);
    $notification->headers[] = 'X-WindowsPhone-Target : toast';
    $notification->headers[] = 'X-NotificationClass : 2';
    $hub->sendNotification($notification, null);


### <a name="kindle-fire"></a><span data-ttu-id="03558-140">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="03558-140">Kindle Fire</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

<span data-ttu-id="03558-141">Running your PHP code should produce now a notification appearing on your target device.</span><span class="sxs-lookup"><span data-stu-id="03558-141">Running your PHP code should produce now a notification appearing on your target device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03558-142">Next Steps</span><span class="sxs-lookup"><span data-stu-id="03558-142">Next Steps</span></span>
<span data-ttu-id="03558-143">In this topic, we showed how to create a simple Java REST client for Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="03558-143">In this topic, we showed how to create a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="03558-144">From here you can:</span><span class="sxs-lookup"><span data-stu-id="03558-144">From here you can:</span></span>

* <span data-ttu-id="03558-145">Download the full [PHP REST wrapper sample], which contains all the code above.</span><span class="sxs-lookup"><span data-stu-id="03558-145">Download the full [PHP REST wrapper sample], which contains all the code above.</span></span>
* <span data-ttu-id="03558-146">Continue learning about Notification Hubs tagging feature in the [Breaking News tutorial]</span><span class="sxs-lookup"><span data-stu-id="03558-146">Continue learning about Notification Hubs tagging feature in the [Breaking News tutorial]</span></span>
* <span data-ttu-id="03558-147">Learn about pushing notifications to individual users in [Notify Users tutorial]</span><span class="sxs-lookup"><span data-stu-id="03558-147">Learn about pushing notifications to individual users in [Notify Users tutorial]</span></span>

<span data-ttu-id="03558-148">For more information, see also the [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="03558-148">For more information, see also the [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[PHP REST wrapper sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

