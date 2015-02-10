Virtual IP Mode Commands
========================
Use the following commands to configure virtual IPs.

virtual-ip
----------
Create or modify a virtual IP for reverse proxy (load balancing) or forward proxy.

Use
^^^
For either a load balancing or forward proxy use case, the system requires at least one virtual IP. The virtual IP is a configuration object that represents the interface that clients connect to. You can create as many virtual IPs as you need. For an overview of how virtual IPs are used in a load balancing use case, see LineRate Overview.

We recommend giving each virtual IP a meaningful name that helps identify the virtual IP. For example, you might use the application or service type (such as serving similar web content) or security settings (such as SSL) in the name.

Use to set the IP address or IP address range and port for the virtual IP. This designates the IP addresses that the system will accept traffic for.

.. note:: For most reverse proxy configurations, the IP address of each virtual IP must also be configured as an IP address on the data interface. If the IP address of the virtual IP is not also configured on a data interface, the system displays the following warning when you set the admin status to online: ``WARNING: virtual-ip test2 has ARP reply disabled until the IP address is configured on a system interface``. 

You can set either a specific IP address and port or a range of IP addresses for a specific port. The range includes both addresses you specify as the range start and end. A range cannot overlap any other range on the system for the same port.

If a virtual IP has a specific IP assigned to it that falls within the range of another virtual IP, the system sends all traffic to the virtual IP with the specific IP address.


.. caution:: When attaching a virtual IP to a forward proxy, the virtual IP must not include any of the system's own IP addresses. For a virtual IP with a single IP address, do not set the virtual IP's IP address to one of the system's own IP addresses. For a virtual IP with a range of addresses, you must ensure that the IP address range does not contain any of the system's own IP addresses. This may mean you need to break the virtual IP into multiple virtual IPs. See Configuring a range for a virtual IP with forward proxy for more detail and an example.

The system handles routed virtual IPs. Even if you set a large range of IP addresses for a virtual IP, the system only sends an ARP reply if an IP address in the range is configured on an interface. However, the system will accept traffic for any IP address in the range.

Command Mode
^^^^^^^^^^^^
configure

Syntax
^^^^^^

Create or modify a virtual IP for load balancing
::
    virtual-ip <name>

IPv4 or IPv6 address of interface for client access
::
    virtual-ip <name> ip <addr> <port>

Set the base that the virtual IP will inherit from
::
    virtual-ip <name> ip <addr> <port> base <basename>

Set a range of IPv4 or IPv6 addresses for client access
::
    [no] virtual-ip <name> ip range <startaddr> <endaddr> <port>

Set a range of IPv4 or IPv6 addresses for client access and set the base that the virtual IP will inherit from
::
    [no] virtual-ip <name> ip range <startaddr> <endaddr> <port> base <base_name>

Create or modify a virtual IP base for virtual IPs to inherit
::
    virtual-ip base <name>

Create or modify a virtual IP base for virtual IPs to inherit
::
    no base

Configure version of LineRate to reload

+-------------+----------+---------------------------------------------------------------------------+
| Parameter   | Type     | Description                                                               |
+=============+==========+===========================================================================+
| `addr`      | IPAddr   | IPv4 or IPv6 address for interface configured for client access           |
+-------------+----------+---------------------------------------------------------------------------+
| `baseName`  | Word     | Name of base that the virtual IP will inherit from                        |
+-------------+----------+---------------------------------------------------------------------------+
| `endaddr`   | IPv4Addr | Ending IPv4 or IPv6 address for interface configured for client access    |
+-------------+----------+---------------------------------------------------------------------------+
| `name`      | Word     | Name of the virtual IP                                                    |
+-------------+----------+---------------------------------------------------------------------------+
| `port`      | Integer  | Port number to connect to on the real server                              |
+-------------+----------+---------------------------------------------------------------------------+
| `startaddr` | IPv4Addr | Starting IPv4 or IPv6 address for interface configured for client access  |
+-------------+----------+---------------------------------------------------------------------------+

Related Commands
^^^^^^^^^^^^^^^^
#. REST API Reference - virtualIP


admin-status
------------
Bring an object, such as a health monitor, real server, or virtual IP, online or offline. After you create an object, you must bring it online.

Use
^^^
You typically set the offline status only when you want to disable the object or block connections to the web server during maintenance or system reconfiguration.

Default Setting
^^^^^^^^^^^^^^^
offline
