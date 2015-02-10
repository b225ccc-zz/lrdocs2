Upgrade Command
------------------

boot
^^^^
Configure version to use to reload the system.

Use
"""
Whenever you upgrade LR, the system retains the previous version, including all configuration settings at the time of the upgrade. If needed, you can reload any previous version by setting the version you want to reload using the boot command.

To see the previous versions available, use the following commands:
::
    bash "ls /base/persist"

.. note::  Be sure to use **write** to save your change after using the boot command, then use reload to actually **reload** to the specified version.

Default Setting
"""""""""""""""
Current system software version

Command Mode
""""""""""""
configure

Syntax
""""""

.. code::

    boot system <version>

Configure version of LR to reload

+------------+--------+--------------------+
| Parameter  | Type   | Description        |
+============+========+====================+
| `version`  | String | Version to reload  |
+------------+--------+--------------------+

Related Commands
""""""""""""""""

Reload Mode Commands

Upgrade Command

REST API Reference - boot
