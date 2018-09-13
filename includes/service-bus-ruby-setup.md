## <a name="create-a-ruby-application"></a><span data-ttu-id="ae67b-101">Create a Ruby application</span><span class="sxs-lookup"><span data-stu-id="ae67b-101">Create a Ruby application</span></span>
<span data-ttu-id="ae67b-102">For instructions, see [Create a Ruby Application on Azure](../articles/virtual-machines/linux/classic/ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="ae67b-102">For instructions, see [Create a Ruby Application on Azure](../articles/virtual-machines/linux/classic/ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="ae67b-103">Configure Your application to Use Service Bus</span><span class="sxs-lookup"><span data-stu-id="ae67b-103">Configure Your application to Use Service Bus</span></span>
<span data-ttu-id="ae67b-104">To use Service Bus, download and use the Azure Ruby package, which includes a set of convenience libraries that communicate with the storage REST services.</span><span class="sxs-lookup"><span data-stu-id="ae67b-104">To use Service Bus, download and use the Azure Ruby package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="ae67b-105">Use RubyGems to obtain the package</span><span class="sxs-lookup"><span data-stu-id="ae67b-105">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="ae67b-106">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="ae67b-106">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="ae67b-107">Type "gem install azure" in the command window to install the gem and dependencies.</span><span class="sxs-lookup"><span data-stu-id="ae67b-107">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="ae67b-108">Import the package</span><span class="sxs-lookup"><span data-stu-id="ae67b-108">Import the package</span></span>
<span data-ttu-id="ae67b-109">Using your favorite text editor, add the following to the top of the Ruby file in which you intend to use storage:</span><span class="sxs-lookup"><span data-stu-id="ae67b-109">Using your favorite text editor, add the following to the top of the Ruby file in which you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="ae67b-110">Set up a Service Bus connection</span><span class="sxs-lookup"><span data-stu-id="ae67b-110">Set up a Service Bus connection</span></span>
<span data-ttu-id="ae67b-111">Use the following code to set the values of namespace, name of the key, key, signer and host:</span><span class="sxs-lookup"><span data-stu-id="ae67b-111">Use the following code to set the values of namespace, name of the key, key, signer and host:</span></span>

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

<span data-ttu-id="ae67b-112">Set the namespace value to the value you created rather than the entire URL.</span><span class="sxs-lookup"><span data-stu-id="ae67b-112">Set the namespace value to the value you created rather than the entire URL.</span></span> <span data-ttu-id="ae67b-113">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span><span class="sxs-lookup"><span data-stu-id="ae67b-113">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span></span>
