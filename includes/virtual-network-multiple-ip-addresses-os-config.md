## <a name="os-config"></a><span data-ttu-id="5e59a-101">Add IP addresses to a VM operating system</span><span class="sxs-lookup"><span data-stu-id="5e59a-101">Add IP addresses to a VM operating system</span></span>

<span data-ttu-id="5e59a-102">Connect and login to a VM you created with multiple private IP addresses.</span><span class="sxs-lookup"><span data-stu-id="5e59a-102">Connect and login to a VM you created with multiple private IP addresses.</span></span> <span data-ttu-id="5e59a-103">You must manually add all the private IP addresses (including the primary) that you added to the VM.</span><span class="sxs-lookup"><span data-stu-id="5e59a-103">You must manually add all the private IP addresses (including the primary) that you added to the VM.</span></span> <span data-ttu-id="5e59a-104">Complete the following steps for your VM operating system:</span><span class="sxs-lookup"><span data-stu-id="5e59a-104">Complete the following steps for your VM operating system:</span></span>

### <a name="windows"></a><span data-ttu-id="5e59a-105">Windows</span><span class="sxs-lookup"><span data-stu-id="5e59a-105">Windows</span></span>

1. <span data-ttu-id="5e59a-106">From a command prompt, type *ipconfig /all*.</span><span class="sxs-lookup"><span data-stu-id="5e59a-106">From a command prompt, type *ipconfig /all*.</span></span>  <span data-ttu-id="5e59a-107">You only see the *Primary* private IP address (through DHCP).</span><span class="sxs-lookup"><span data-stu-id="5e59a-107">You only see the *Primary* private IP address (through DHCP).</span></span>
2. <span data-ttu-id="5e59a-108">Type *ncpa.cpl* in the command prompt to open the **Network connections** window.</span><span class="sxs-lookup"><span data-stu-id="5e59a-108">Type *ncpa.cpl* in the command prompt to open the **Network connections** window.</span></span>
3. <span data-ttu-id="5e59a-109">Open the properties for the appropriate adapter: **Local Area Connection**.</span><span class="sxs-lookup"><span data-stu-id="5e59a-109">Open the properties for the appropriate adapter: **Local Area Connection**.</span></span>
4. <span data-ttu-id="5e59a-110">Double-click Internet Protocol version 4 (IPv4).</span><span class="sxs-lookup"><span data-stu-id="5e59a-110">Double-click Internet Protocol version 4 (IPv4).</span></span>
5. <span data-ttu-id="5e59a-111">Select **Use the following IP address** and enter the following values:</span><span class="sxs-lookup"><span data-stu-id="5e59a-111">Select **Use the following IP address** and enter the following values:</span></span>

    * <span data-ttu-id="5e59a-112">**IP address**: Enter the *Primary* private IP address</span><span class="sxs-lookup"><span data-stu-id="5e59a-112">**IP address**: Enter the *Primary* private IP address</span></span>
    * <span data-ttu-id="5e59a-113">**Subnet mask**: Set based on your subnet.</span><span class="sxs-lookup"><span data-stu-id="5e59a-113">**Subnet mask**: Set based on your subnet.</span></span> <span data-ttu-id="5e59a-114">For example, if the subnet is a /24 subnet then the subnet mask is 255.255.255.0.</span><span class="sxs-lookup"><span data-stu-id="5e59a-114">For example, if the subnet is a /24 subnet then the subnet mask is 255.255.255.0.</span></span>
    * <span data-ttu-id="5e59a-115">**Default gateway**: The first IP address in the subnet.</span><span class="sxs-lookup"><span data-stu-id="5e59a-115">**Default gateway**: The first IP address in the subnet.</span></span> <span data-ttu-id="5e59a-116">If your subnet is 10.0.0.0/24, then the gateway IP address is 10.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="5e59a-116">If your subnet is 10.0.0.0/24, then the gateway IP address is 10.0.0.1.</span></span>
    * <span data-ttu-id="5e59a-117">Click **Use the following DNS server addresses** and enter the following values:</span><span class="sxs-lookup"><span data-stu-id="5e59a-117">Click **Use the following DNS server addresses** and enter the following values:</span></span>
        * <span data-ttu-id="5e59a-118">**Preferred DNS server**: If you are not using your own DNS server, enter 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="5e59a-118">**Preferred DNS server**: If you are not using your own DNS server, enter 168.63.129.16.</span></span>  <span data-ttu-id="5e59a-119">If you are using your own DNS server, enter the IP address for your server.</span><span class="sxs-lookup"><span data-stu-id="5e59a-119">If you are using your own DNS server, enter the IP address for your server.</span></span>
    * <span data-ttu-id="5e59a-120">Click the **Advanced** button and add additional IP addresses.</span><span class="sxs-lookup"><span data-stu-id="5e59a-120">Click the **Advanced** button and add additional IP addresses.</span></span> <span data-ttu-id="5e59a-121">Add each of the secondary private IP addresses listed in step 8 to the NIC with the same subnet specified for the primary IP address.</span><span class="sxs-lookup"><span data-stu-id="5e59a-121">Add each of the secondary private IP addresses listed in step 8 to the NIC with the same subnet specified for the primary IP address.</span></span>
        >[!WARNING] 
        ><span data-ttu-id="5e59a-122">If you do not follow the steps above correctly, you may lose connectivity to your VM.</span><span class="sxs-lookup"><span data-stu-id="5e59a-122">If you do not follow the steps above correctly, you may lose connectivity to your VM.</span></span> <span data-ttu-id="5e59a-123">Ensure the information entered for step 5 is accurate before proceeding.</span><span class="sxs-lookup"><span data-stu-id="5e59a-123">Ensure the information entered for step 5 is accurate before proceeding.</span></span>

    * <span data-ttu-id="5e59a-124">Click **OK** to close out the TCP/IP settings and then **OK** again to close the adapter settings.</span><span class="sxs-lookup"><span data-stu-id="5e59a-124">Click **OK** to close out the TCP/IP settings and then **OK** again to close the adapter settings.</span></span> <span data-ttu-id="5e59a-125">Your RDP connection is re-established.</span><span class="sxs-lookup"><span data-stu-id="5e59a-125">Your RDP connection is re-established.</span></span>

6. <span data-ttu-id="5e59a-126">From a command prompt, type *ipconfig /all*.</span><span class="sxs-lookup"><span data-stu-id="5e59a-126">From a command prompt, type *ipconfig /all*.</span></span> <span data-ttu-id="5e59a-127">All IP addresses you added are shown and DHCP is turned off.</span><span class="sxs-lookup"><span data-stu-id="5e59a-127">All IP addresses you added are shown and DHCP is turned off.</span></span>


### <a name="validation-windows"></a><span data-ttu-id="5e59a-128">Validation (Windows)</span><span class="sxs-lookup"><span data-stu-id="5e59a-128">Validation (Windows)</span></span>

<span data-ttu-id="5e59a-129">To ensure you are able to connect to the internet from your secondary IP configuration via the public IP associated it, once you have added it correctly using steps above, use the following command:</span><span class="sxs-lookup"><span data-stu-id="5e59a-129">To ensure you are able to connect to the internet from your secondary IP configuration via the public IP associated it, once you have added it correctly using steps above, use the following command:</span></span>

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="5e59a-130">You can only ping to the internet if the private IP address you are using above has a public IP associated with it.</span><span class="sxs-lookup"><span data-stu-id="5e59a-130">You can only ping to the internet if the private IP address you are using above has a public IP associated with it.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="5e59a-131">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="5e59a-131">Linux (Ubuntu)</span></span>

1. <span data-ttu-id="5e59a-132">Open a terminal window.</span><span class="sxs-lookup"><span data-stu-id="5e59a-132">Open a terminal window.</span></span>
2. <span data-ttu-id="5e59a-133">Make sure you are the root user.</span><span class="sxs-lookup"><span data-stu-id="5e59a-133">Make sure you are the root user.</span></span> <span data-ttu-id="5e59a-134">If you are not, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="5e59a-134">If you are not, enter the following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="5e59a-135">Update the configuration file of the network interface (assuming ‘eth0’).</span><span class="sxs-lookup"><span data-stu-id="5e59a-135">Update the configuration file of the network interface (assuming ‘eth0’).</span></span>

    * <span data-ttu-id="5e59a-136">Keep the existing line item for dhcp.</span><span class="sxs-lookup"><span data-stu-id="5e59a-136">Keep the existing line item for dhcp.</span></span> <span data-ttu-id="5e59a-137">The primary IP address remains configured as it was previously.</span><span class="sxs-lookup"><span data-stu-id="5e59a-137">The primary IP address remains configured as it was previously.</span></span>
    * <span data-ttu-id="5e59a-138">Add a configuration for an additional static IP address with the following commands:</span><span class="sxs-lookup"><span data-stu-id="5e59a-138">Add a configuration for an additional static IP address with the following commands:</span></span>

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    <span data-ttu-id="5e59a-139">You should see a .cfg file.</span><span class="sxs-lookup"><span data-stu-id="5e59a-139">You should see a .cfg file.</span></span>
4. <span data-ttu-id="5e59a-140">Open the file.</span><span class="sxs-lookup"><span data-stu-id="5e59a-140">Open the file.</span></span> <span data-ttu-id="5e59a-141">You should see the following lines at the end of the file:</span><span class="sxs-lookup"><span data-stu-id="5e59a-141">You should see the following lines at the end of the file:</span></span>

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. <span data-ttu-id="5e59a-142">Add the following lines after the lines that exist in this file:</span><span class="sxs-lookup"><span data-stu-id="5e59a-142">Add the following lines after the lines that exist in this file:</span></span>

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. <span data-ttu-id="5e59a-143">Save the file by using the following command:</span><span class="sxs-lookup"><span data-stu-id="5e59a-143">Save the file by using the following command:</span></span>

    ```bash
    :wq
    ```

7. <span data-ttu-id="5e59a-144">Reset the network interface with the following command:</span><span class="sxs-lookup"><span data-stu-id="5e59a-144">Reset the network interface with the following command:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="5e59a-145">Run both ifdown and ifup in the same line if using a remote connection.</span><span class="sxs-lookup"><span data-stu-id="5e59a-145">Run both ifdown and ifup in the same line if using a remote connection.</span></span>
    >

8. <span data-ttu-id="5e59a-146">Verify the IP address is added to the network interface with the following command:</span><span class="sxs-lookup"><span data-stu-id="5e59a-146">Verify the IP address is added to the network interface with the following command:</span></span>

    ```bash
    ip addr list eth0
    ```

    <span data-ttu-id="5e59a-147">You should see the IP address you added as part of the list.</span><span class="sxs-lookup"><span data-stu-id="5e59a-147">You should see the IP address you added as part of the list.</span></span>

### <a name="linux-redhat-centos-and-others"></a><span data-ttu-id="5e59a-148">Linux (Redhat, CentOS, and others)</span><span class="sxs-lookup"><span data-stu-id="5e59a-148">Linux (Redhat, CentOS, and others)</span></span>

1. <span data-ttu-id="5e59a-149">Open a terminal window.</span><span class="sxs-lookup"><span data-stu-id="5e59a-149">Open a terminal window.</span></span>
2. <span data-ttu-id="5e59a-150">Make sure you are the root user.</span><span class="sxs-lookup"><span data-stu-id="5e59a-150">Make sure you are the root user.</span></span> <span data-ttu-id="5e59a-151">If you are not, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="5e59a-151">If you are not, enter the following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="5e59a-152">Enter your password and follow instructions as prompted.</span><span class="sxs-lookup"><span data-stu-id="5e59a-152">Enter your password and follow instructions as prompted.</span></span> <span data-ttu-id="5e59a-153">Once you are the root user, navigate to the network scripts folder with the following command:</span><span class="sxs-lookup"><span data-stu-id="5e59a-153">Once you are the root user, navigate to the network scripts folder with the following command:</span></span>

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. <span data-ttu-id="5e59a-154">List the related ifcfg files using the following command:</span><span class="sxs-lookup"><span data-stu-id="5e59a-154">List the related ifcfg files using the following command:</span></span>

    ```bash
    ls ifcfg-*
    ```

    <span data-ttu-id="5e59a-155">You should see *ifcfg-eth0* as one of the files.</span><span class="sxs-lookup"><span data-stu-id="5e59a-155">You should see *ifcfg-eth0* as one of the files.</span></span>

5. <span data-ttu-id="5e59a-156">To add an IP address, create a configuration file for it as shown below.</span><span class="sxs-lookup"><span data-stu-id="5e59a-156">To add an IP address, create a configuration file for it as shown below.</span></span> <span data-ttu-id="5e59a-157">Note that one file must be created for each IP configuration.</span><span class="sxs-lookup"><span data-stu-id="5e59a-157">Note that one file must be created for each IP configuration.</span></span>

    ```bash
    touch ifcfg-eth0:0
    ```

6. <span data-ttu-id="5e59a-158">Open the *ifcfg-eth0:0* file with the following command:</span><span class="sxs-lookup"><span data-stu-id="5e59a-158">Open the *ifcfg-eth0:0* file with the following command:</span></span>

    ```bash
    vi ifcfg-eth0:0
    ```

7. <span data-ttu-id="5e59a-159">Add content to the file, *eth0:0* in this case, with the following command.</span><span class="sxs-lookup"><span data-stu-id="5e59a-159">Add content to the file, *eth0:0* in this case, with the following command.</span></span> <span data-ttu-id="5e59a-160">Be sure to update information based on your IP address.</span><span class="sxs-lookup"><span data-stu-id="5e59a-160">Be sure to update information based on your IP address.</span></span>

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. <span data-ttu-id="5e59a-161">Save the file with the following command:</span><span class="sxs-lookup"><span data-stu-id="5e59a-161">Save the file with the following command:</span></span>

    ```bash
    :wq
    ```

9. <span data-ttu-id="5e59a-162">Restart the network services and make sure the changes are successful by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="5e59a-162">Restart the network services and make sure the changes are successful by running the following commands:</span></span>

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    <span data-ttu-id="5e59a-163">You should see the IP address you added, *eth0:0*, in the list returned.</span><span class="sxs-lookup"><span data-stu-id="5e59a-163">You should see the IP address you added, *eth0:0*, in the list returned.</span></span>

### <a name="validation-linux"></a><span data-ttu-id="5e59a-164">Validation (Linux)</span><span class="sxs-lookup"><span data-stu-id="5e59a-164">Validation (Linux)</span></span>

<span data-ttu-id="5e59a-165">To ensure you are able to connect to the internet from your secondary IP configuration via the public IP associated it, use the following command:</span><span class="sxs-lookup"><span data-stu-id="5e59a-165">To ensure you are able to connect to the internet from your secondary IP configuration via the public IP associated it, use the following command:</span></span>

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="5e59a-166">You can only ping to the internet if the private IP address you are using above has a public IP associated with it.</span><span class="sxs-lookup"><span data-stu-id="5e59a-166">You can only ping to the internet if the private IP address you are using above has a public IP associated with it.</span></span>

<span data-ttu-id="5e59a-167">For Linux VMs, when trying to validate outbound connectivity from a secondary NIC, you may need to add appropriate routes.</span><span class="sxs-lookup"><span data-stu-id="5e59a-167">For Linux VMs, when trying to validate outbound connectivity from a secondary NIC, you may need to add appropriate routes.</span></span> <span data-ttu-id="5e59a-168">There are many ways to do this.</span><span class="sxs-lookup"><span data-stu-id="5e59a-168">There are many ways to do this.</span></span> <span data-ttu-id="5e59a-169">Please see appropriate documentation for your Linux distribution.</span><span class="sxs-lookup"><span data-stu-id="5e59a-169">Please see appropriate documentation for your Linux distribution.</span></span> <span data-ttu-id="5e59a-170">The following is one method to accomplish this:</span><span class="sxs-lookup"><span data-stu-id="5e59a-170">The following is one method to accomplish this:</span></span>

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- <span data-ttu-id="5e59a-171">Be sure to replace:</span><span class="sxs-lookup"><span data-stu-id="5e59a-171">Be sure to replace:</span></span>
    - <span data-ttu-id="5e59a-172">**10.0.0.5** with the private IP address that has a public IP address associated to it</span><span class="sxs-lookup"><span data-stu-id="5e59a-172">**10.0.0.5** with the private IP address that has a public IP address associated to it</span></span>
    - <span data-ttu-id="5e59a-173">**10.0.0.1** to your default gateway</span><span class="sxs-lookup"><span data-stu-id="5e59a-173">**10.0.0.1** to your default gateway</span></span>
    - <span data-ttu-id="5e59a-174">**eth2** to the name of your secondary NIC</span><span class="sxs-lookup"><span data-stu-id="5e59a-174">**eth2** to the name of your secondary NIC</span></span>
