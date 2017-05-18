========================
Infortrend Manila driver
========================

The `Infortrend <http://www.infortrend.com/global>`__ Manila driver
provides NFS and CIFS shared file systems to Openstack.

Requirements
~~~~~~~~~~~~

To use the Infortrend Manila driver, the followings are required:

- GS/GSe Family firmware version v73.1.0-4 and later.

- Configure at least one channel for shared file systems.

Supported shared filesystems and operations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This driver supports NFS and CIFS shares.

The following operations are supported:

- Create a share.

- Delete a share.

- Allow share access.

  Note the following limitations:

  - Only IP access type is supported for NFS.

  - Only user access type is supported for CIFS.

- Deny share access.

- Manage a share.

- Unmanage a share.

- Extend a share.

- Shrink a share.


Driver configuration
~~~~~~~~~~~~~~~~~~~~

On ``manila-share`` nodes, set the following in your
``/etc/manila/manila.conf``, and use the following options to configure it:

Driver options
--------------

.. list-table:: Description of Infortrend Manila driver configuration options
   :header-rows: 1
   :class: config-ref-table

   * - Configuration option = Default value
     - Description
   * - **[DEFAULT]**
     -
   * - ``infortrend_nas_ip`` = ``None``
     - (String) Infortrend nas ip. It is the ip for management.
   * - ``infortrend_nas_user`` = ``manila``
     - (String) Infortrend nas username.
   * - ``infortrend_nas_password`` = ``None``
     - (String) Infortrend nas password. This is not necessary if infortrend_nas_ssh_key is set.
   * - ``infortrend_nas_ssh_key`` = ``None``
     - (String) Infortrend nas ssh key. This is not necessary if infortrend_nas_password is set.
   * - ``infortrend_share_pools`` = ``None``
     - (String) Infortrend nas pool name list. It is separated with comma.
   * - ``infortrend_share_channels`` = ``None``
     - (String) Infortrend channels for file service. It is separated with comma.
   * - ``infortrend_cli_max_retries`` = ``5``
     - (Integer) Maximum retry times for cli.
   * - ``infortrend_cli_timeout`` = ``30``
     - (Integer) CLI timeout in seconds.

Back-end configuration example
---------------------------

.. code-block:: ini

   [DEFAULT]
   enabled_share_backends = ift-manila
   enabled_share_protocols = NFS, CIFS

   [ift-manila]
   share_backend_name = ift-manila
   share_driver = manila.share.drivers.infortrend.driver.InfortrendNASDriver
   driver_handles_share_servers = False
   infortrend_nas_ip = FAKE_IP
   infortrend_nas_user = FAKE_USER
   infortrend_nas_password = FAKE_PASS
   infortrend_share_pools = pool-1, pool-2
   infortrend_share_channels = 0, 1
