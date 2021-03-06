..
  Warning: Do not edit this file. It is automatically generated and your
  changes will be overwritten. The tool to do so lives in the
  openstack-doc-tools repository.

.. list-table:: Description of configuration options for ``[swift-constraints]`` in ``swift.conf``
   :header-rows: 1
   :class: config-ref-table

   * - Configuration option = Default value
     - Description
   * - ``account_listing_limit`` = ``10000``
     - The default (and maximum) number of items returned for an account listing request.
   * - ``container_listing_limit`` = ``10000``
     - The default (and maximum) number of items returned for a container listing request.
   * - ``extra_header_count`` = ``0``
     - By default the maximum number of allowed headers depends on the number of max allowed metadata settings plus a default value of 32 for regular http headers. If for some reason this is not enough (custom middleware for example) it can be increased with the extra_header_count constraint.
   * - ``max_account_name_length`` = ``256``
     - The maximum number of bytes in the utf8 encoding of an account name.
   * - ``max_container_name_length`` = ``256``
     - The maximum number of bytes in the utf8 encoding of a container name.
   * - ``max_file_size`` = ``5368709122``
     - The largest normal object that can be saved in the cluster. This is also the limit on the size of each segment of a large object when using the large object manifest support. This value is set in bytes. Setting it to lower than 1MiB will cause some tests to fail. It is STRONGLY recommended to leave this value at the default (5 * 2**30 + 2).
   * - ``max_header_size`` = ``8192``
     - The max number of bytes in the utf8 encoding of each header. Using 8192 as default because eventlet use 8192 as maximum size of header line. You may need to increase this value when using identity v3 API tokens including more than 7 catalog entries. See also include_service_catalog in proxy-server.conf-sample (documented in overview_auth.rst).
   * - ``max_meta_count`` = ``90``
     - The max number of metadata keys that can be stored on a single account, container, or object.
   * - ``max_meta_name_length`` = ``128``
     - The max number of bytes in the utf8 encoding of the name portion of a metadata header.
   * - ``max_meta_overall_size`` = ``4096``
     - The max number of bytes in the utf8 encoding of the metadata (keys + values).
   * - ``max_meta_value_length`` = ``256``
     - The max number of bytes in the utf8 encoding of a metadata value.
   * - ``max_object_name_length`` = ``1024``
     - The max number of bytes in the utf8 encoding of an object name.
   * - ``valid_api_versions`` = ``v0,v1,v2``
     - No help text available for this option.
