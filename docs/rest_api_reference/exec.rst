=========================
/exec/system/util/upgrade
=========================
Upgrade the system software

Usage
----------
Use to upgrade LROS software to a new version. The upgrade will retain all of your configuration and lets you roll back to a previously installed software version using either of the following:

- CLI command: ``boot system``
- REST node: ``/config/system/boot/version``

.. note:: To subscribe to software release notifications, contact your sales account representative.

Download the upgrade file, which has the extension ``.upg.gz``, to the LineRate system or to a web server on your intranet. For where to go to download the upgrade file, see Downloads.

If you download the file to a web server on your intranet, you can copy the file to your LineRate system one of the following ways:

- Use ``scp`` to copy the file to the ``/home/linerate`` directory
- Use the following REST node: ``/exec/system/util/download``

.. caution:: We recommend upgrading during a maintenance window.  **The upgrade process causes a system reload.**  During the reload, you will lose all connections to the LineRate system for at least a few minutes.

The upgrade command may also be used to install an earlier version of software (to "downgrade") in limited circumstances. If the earlier version of software is already installed, you should use the boot system command to switch to that version of software. If the earlier version of software is not installed, the LineRate only supports installing the maintenance release immediately prior to the currently running software version via the upgrade process. To find the prior version of software that can be used with the upgrade process, see the release notes for your currently running software version.

Request Format
~~~~~~~~~~~~~~~~~

+-----------------------+------------+
| **Supported Methods** | ``PUT``    |
+-----------------------+------------+
| **Default Allowed**   | ``False``  |
+-----------------------+------------+

Data
********

+----------------------+------------+
| **Data Type**        | ``json``   |
+----------------------+------------+
| **Default Value**    | ``""``     |
+----------------------+------------+

Parameters

+---------------+----------+---------------------------------------------------------------------------+
| Name          | Type     | Description                                                               |
+===============+==========+===========================================================================+
| ``img``       | string   | The path of the downloaded upgrade image                                  |
+---------------+----------+---------------------------------------------------------------------------+
| ``filename``  | string   | The name of the upgrade file                                              |
+---------------+----------+---------------------------------------------------------------------------+

Example - PUT
~~~~~~~~~~~~~~~~~

Request
::
    curl -b cookie.jar --data @data.json -k -H "Content-Type: application/json" -X PUT https://10.1.2.3:8443/lrs/api/v1.0/exec/system/util/upgrade

Response
::
    {
      "httpResponseCode": 200,
      "requestPath": "/exec/system/util/upgrade",
      "recurse": false
    }

data.json
::
    { 
      "data": {
        "img": "/tmp/upgrade.img.gz",
        "filename": "upgrade.img.gz"
      },
      "type": "json",
      "default": false
    }
