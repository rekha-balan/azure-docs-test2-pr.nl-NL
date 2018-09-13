### <a name="create-a-nodejs-application"></a><span data-ttu-id="e76fa-101">Create a Node.js application</span><span class="sxs-lookup"><span data-stu-id="e76fa-101">Create a Node.js application</span></span>
* <span data-ttu-id="e76fa-102">Create a new JavaScript file called `sender.js`.</span><span class="sxs-lookup"><span data-stu-id="e76fa-102">Create a new JavaScript file called `sender.js`.</span></span>

### <a name="add-the-relay-npm-package"></a><span data-ttu-id="e76fa-103">Add the Relay NPM package</span><span class="sxs-lookup"><span data-stu-id="e76fa-103">Add the Relay NPM package</span></span>
* <span data-ttu-id="e76fa-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span><span class="sxs-lookup"><span data-stu-id="e76fa-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-to-send-messages"></a><span data-ttu-id="e76fa-105">Write some code to send messages</span><span class="sxs-lookup"><span data-stu-id="e76fa-105">Write some code to send messages</span></span>
1. <span data-ttu-id="e76fa-106">Add the following `constants` to the top of the `sender.js` file.</span><span class="sxs-lookup"><span data-stu-id="e76fa-106">Add the following `constants` to the top of the `sender.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. <span data-ttu-id="e76fa-107">Add the following Relay `constants` to the `sender.js` for the Hybrid Connection connection details.</span><span class="sxs-lookup"><span data-stu-id="e76fa-107">Add the following Relay `constants` to the `sender.js` for the Hybrid Connection connection details.</span></span> <span data-ttu-id="e76fa-108">Replace the placeholders in brackets with the proper values that were obtained when creating the Hybrid Connection.</span><span class="sxs-lookup"><span data-stu-id="e76fa-108">Replace the placeholders in brackets with the proper values that were obtained when creating the Hybrid Connection.</span></span>
   
   1. <span data-ttu-id="e76fa-109">`const ns` - The Relay namespace (use FQDN - e.g. `{namespace}.servicebus.windows.net`)</span><span class="sxs-lookup"><span data-stu-id="e76fa-109">`const ns` - The Relay namespace (use FQDN - e.g. `{namespace}.servicebus.windows.net`)</span></span>
   2. <span data-ttu-id="e76fa-110">`const path` - The name of the Hybrid Connection</span><span class="sxs-lookup"><span data-stu-id="e76fa-110">`const path` - The name of the Hybrid Connection</span></span>
   3. <span data-ttu-id="e76fa-111">`const keyrule` - The name of the SAS key</span><span class="sxs-lookup"><span data-stu-id="e76fa-111">`const keyrule` - The name of the SAS key</span></span>
   4. <span data-ttu-id="e76fa-112">`const key` - The SAS key value</span><span class="sxs-lookup"><span data-stu-id="e76fa-112">`const key` - The SAS key value</span></span>
3. <span data-ttu-id="e76fa-113">Add the following code to the `sender.js` file:</span><span class="sxs-lookup"><span data-stu-id="e76fa-113">Add the following code to the `sender.js` file:</span></span>
   
    ```js
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```
    <span data-ttu-id="e76fa-114">Here is what your listener.js should look like:</span><span class="sxs-lookup"><span data-stu-id="e76fa-114">Here is what your listener.js should look like:</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```

