### <a name="what-operating-systems-can-i-use-with-point-to-site"></a>What operating systems can I use with Point-to-Site?
The following operating systems are supported:

* Windows 7 (32-bit and 64-bit)
* Windows Server 2008 R2 (64-bit only)
* Windows 8 (32-bit and 64-bit)
* Windows 8.1 (32-bit and 64-bit)
* Windows Server 2012 (64-bit only)
* Windows Server 2012 R2 (64-bit only)
* Windows 10

### <a name="can-i-use-any-software-vpn-client-for-point-to-site-that-supports-sstp"></a>Can I use any software VPN client for Point-to-Site that supports SSTP?
No. Support is limited only to the Windows operating system versions listed above.

### <a name="how-many-vpn-client-endpoints-can-i-have-in-my-point-to-site-configuration"></a>How many VPN client endpoints can I have in my Point-to-Site configuration?
We support up to 128 VPN clients to be able to connect to a virtual network at the same time.

### <a name="can-i-use-my-own-internal-pki-root-ca-for-point-to-site-connectivity"></a>Can I use my own internal PKI root CA for Point-to-Site connectivity?
Yes. Previously, only self-signed root certificates could be used. You can still upload 20 root certificates.

### <a name="can-i-traverse-proxies-and-firewalls-using-point-to-site-capability"></a>Can I traverse proxies and firewalls using Point-to-Site capability?
Yes. We use SSTP (Secure Socket Tunneling Protocol) to tunnel through firewalls. This tunnel will appear as an HTTPs connection.

### <a name="if-i-restart-a-client-computer-configured-for-point-to-site-will-the-vpn-automatically-reconnect"></a>If I restart a client computer configured for Point-to-Site, will the VPN automatically reconnect?
By default, the client computer will not reestablish the VPN connection automatically.

### <a name="does-point-to-site-support-auto-reconnect-and-ddns-on-the-vpn-clients"></a>Does Point-to-Site support auto-reconnect and DDNS on the VPN clients?
Auto-reconnect and DDNS are currently not supported in Point-to-Site VPNs.

### <a name="can-i-have-site-to-site-and-point-to-site-configurations-coexist-for-the-same-virtual-network"></a>Can I have Site-to-Site and Point-to-Site configurations coexist for the same virtual network?
Yes. Both these solutions will work if you have a RouteBased VPN type for your gateway. For the classic deployment model, you need a dynamic gateway. We do not support Point-to-Site for static routing VPN gateways or gateways using the `-VpnType PolicyBased` cmdlet.

### <a name="can-i-configure-a-point-to-site-client-to-connect-to-multiple-virtual-networks-at-the-same-time"></a>Can I configure a Point-to-Site client to connect to multiple virtual networks at the same time?
Yes, it is possible. But the virtual networks cannot have overlapping IP prefixes and the Point-to-Site address spaces must not overlap between the virtual networks.

### <a name="how-much-throughput-can-i-expect-through-site-to-site-or-point-to-site-connections"></a>How much throughput can I expect through Site-to-Site or Point-to-Site connections?
It's difficult to maintain the exact throughput of the VPN tunnels. IPsec and SSTP are crypto-heavy VPN protocols. Throughput is also limited by the latency and bandwidth between your premises and the Internet.