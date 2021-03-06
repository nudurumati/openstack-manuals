..
    Warning: Do not edit this file. It is automatically generated from the
    software project's code and your changes will be overwritten.

    The tool to generate this file lives in openstack-doc-tools repository.

    Please make any changes needed in the code, then run the
    autogenerate-config-doc tool from the openstack-doc-tools repository, or
    ask for help on the documentation mailing list, IRC channel or meeting.

.. _ironic-common:

.. list-table:: Description of common configuration options
   :header-rows: 1
   :class: config-ref-table

   * - Configuration option = Default value
     - Description
   * - **[DEFAULT]**
     -
   * - ``bindir`` = ``/usr/local/bin``
     - (String) Directory where ironic binaries are installed.
   * - ``debug_tracebacks_in_api`` = ``False``
     - (Boolean) Return server tracebacks in the API response for any error responses. WARNING: this is insecure and should not be used in a production environment.
   * - ``default_network_interface`` = ``None``
     - (String) Default network interface to be used for nodes that do not have network_interface field set. A complete list of network interfaces present on your system may be found by enumerating the "ironic.hardware.interfaces.network" entrypoint.
   * - ``enabled_drivers`` = ``pxe_ipmitool``
     - (List) Specify the list of drivers to load during service initialization. Missing drivers, or drivers which fail to initialize, will prevent the conductor service from starting. The option default is a recommended set of production-oriented drivers. A complete list of drivers present on your system may be found by enumerating the "ironic.drivers" entrypoint. An example may be found in the developer documentation online.
   * - ``enabled_network_interfaces`` = ``flat, noop``
     - (List) Specify the list of network interfaces to load during service initialization. Missing network interfaces, or network interfaces which fail to initialize, will prevent the conductor service from starting. The option default is a recommended set of production-oriented network interfaces. A complete list of network interfaces present on your system may be found by enumerating the "ironic.hardware.interfaces.network" entrypoint. This value must be the same on all ironic-conductor and ironic-api services, because it is used by ironic-api service to validate a new or updated node's network_interface value.
   * - ``executor_thread_pool_size`` = ``64``
     - (Integer) Size of executor thread pool.
   * - ``fatal_exception_format_errors`` = ``False``
     - (Boolean) Used if there is a formatting error when generating an exception message (a programming error). If True, raise an exception; if False, use the unformatted message.
   * - ``force_raw_images`` = ``True``
     - (Boolean) If True, convert backing images to "raw" disk image format.
   * - ``grub_config_template`` = ``$pybasedir/common/grub_conf.template``
     - (String) Template file for grub configuration file.
   * - ``hash_distribution_replicas`` = ``1``
     - (Integer) [Experimental Feature] Number of hosts to map onto each hash partition. Setting this to more than one will cause additional conductor services to prepare deployment environments and potentially allow the Ironic cluster to recover more quickly if a conductor instance is terminated.
   * - ``hash_partition_exponent`` = ``5``
     - (Integer) Exponent to determine number of hash partitions to use when distributing load across conductors. Larger values will result in more even distribution of load and less load when rebalancing the ring, but more memory usage. Number of partitions per conductor is (2^hash_partition_exponent). This determines the granularity of rebalancing: given 10 hosts, and an exponent of the 2, there are 40 partitions in the ring.A few thousand partitions should make rebalancing smooth in most cases. The default is suitable for up to a few hundred conductors. Too many partitions has a CPU impact.
   * - ``hash_ring_reset_interval`` = ``180``
     - (Integer) Interval (in seconds) between hash ring resets.
   * - ``host`` = ``localhost``
     - (String) Name of this node. This can be an opaque identifier. It is not necessarily a hostname, FQDN, or IP address. However, the node name must be valid within an AMQP key, and if using ZeroMQ, a valid hostname, FQDN, or IP address.
   * - ``isolinux_bin`` = ``/usr/lib/syslinux/isolinux.bin``
     - (String) Path to isolinux binary file.
   * - ``isolinux_config_template`` = ``$pybasedir/common/isolinux_config.template``
     - (String) Template file for isolinux configuration file.
   * - ``my_ip`` = ``127.0.0.1``
     - (String) IP address of this host. If unset, will determine the IP programmatically. If unable to do so, will use "127.0.0.1".
   * - ``notification_level`` = ``None``
     - (String) Specifies the minimum level for which to send notifications. If not set, no notifications will be sent. The default is for this option to be unset.
   * - ``parallel_image_downloads`` = ``False``
     - (Boolean) Run image downloads and raw format conversions in parallel.
   * - ``pybasedir`` = ``/usr/lib/python/site-packages/ironic/ironic``
     - (String) Directory where the ironic python module is installed.
   * - ``rootwrap_config`` = ``/etc/ironic/rootwrap.conf``
     - (String) Path to the rootwrap configuration file to use for running commands as root.
   * - ``state_path`` = ``$pybasedir``
     - (String) Top-level directory for maintaining ironic's state.
   * - ``tempdir`` = ``/tmp``
     - (String) Temporary working directory, default is Python temp dir.
   * - **[ironic_lib]**
     -
   * - ``fatal_exception_format_errors`` = ``False``
     - (Boolean) Make exception message format errors fatal.
   * - ``root_helper`` = ``sudo ironic-rootwrap /etc/ironic/rootwrap.conf``
     - (String) Command that is prefixed to commands that are run as root. If not specified, no commands are run as root.
