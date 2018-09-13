### <a name="create-a-nodejs-application"></a><span data-ttu-id="ba4aa-101">Create a Node.js application</span><span class="sxs-lookup"><span data-stu-id="ba4aa-101">Create a Node.js application</span></span>
* <span data-ttu-id="ba4aa-102">Create a new JavaScript file called `listener.js`.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-102">Create a new JavaScript file called `listener.js`.</span></span>

### <a name="add-the-relay-npm-package"></a><span data-ttu-id="ba4aa-103">Add the Relay NPM package</span><span class="sxs-lookup"><span data-stu-id="ba4aa-103">Add the Relay NPM package</span></span>
* <span data-ttu-id="ba4aa-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-to-receive-messages"></a><span data-ttu-id="ba4aa-105">Write some code to receive messages</span><span class="sxs-lookup"><span data-stu-id="ba4aa-105">Write some code to receive messages</span></span>
1. <span data-ttu-id="ba4aa-106">Add the following `constant` to the top of the `listener.js` file.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-106">Add the following `constant` to the top of the `listener.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. <span data-ttu-id="ba4aa-107">Add the following Relay `constants` to the `listener.js` for the Hybrid Connection connection details.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-107">Add the following Relay `constants` to the `listener.js` for the Hybrid Connection connection details.</span></span> <span data-ttu-id="ba4aa-108">Replace the placeholders in brackets with the proper values that were obtained when creating the Hybrid Connection.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-108">Replace the placeholders in brackets with the proper values that were obtained when creating the Hybrid Connection.</span></span>
   
   1. <span data-ttu-id="ba4aa-109">`const ns` - The Relay namespace (use FQDN - e.g. `{namespace}.servicebus.windows.net`)</span><span class="sxs-lookup"><span data-stu-id="ba4aa-109">`const ns` - The Relay namespace (use FQDN - e.g. `{namespace}.servicebus.windows.net`)</span></span>
   2. <span data-ttu-id="ba4aa-110">`const path` - The name of the Hybrid Connection</span><span class="sxs-lookup"><span data-stu-id="ba4aa-110">`const path` - The name of the Hybrid Connection</span></span>
   3. <span data-ttu-id="ba4aa-111">`const keyrule` - The name of the SAS key</span><span class="sxs-lookup"><span data-stu-id="ba4aa-111">`const keyrule` - The name of the SAS key</span></span>
   4. <span data-ttu-id="ba4aa-112">`const key` - The SAS key value</span><span class="sxs-lookup"><span data-stu-id="ba4aa-112">`const key` - The SAS key value</span></span>
3. <span data-ttu-id="ba4aa-113">Add the following code to the `listener.js` file:</span><span class="sxs-lookup"><span data-stu-id="ba4aa-113">Add the following code to the `listener.js` file:</span></span>
   
    ```js
    var wss = WebSocket.createRelayedServer(
    {
        server : WebSocket.createRelayListenUri(ns, path),
        token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(event.data);
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```
    <span data-ttu-id="ba4aa-114">Here is what your listener.js should look like:</span><span class="sxs-lookup"><span data-stu-id="ba4aa-114">Here is what your listener.js should look like:</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    var wss = WebSocket.createRelayedServer(
        {
            server : WebSocket.createRelayListenUri(ns, path),
            token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
        }, 
        function (ws) {
            console.log('connection accepted');
            ws.onmessage = function (event) {
                console.log(event.data);
            };
            ws.on('close', function () {
                console.log('connection closed');
            });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```

