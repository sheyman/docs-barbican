
.. _post-container:

Create a container
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /v1/containers

Creates a container.

There are three different types of containers that can be created: generic,
rsa, and certificate.

**Generic**

This type of container holds any number of references to secrets. Each secret
reference is accompanied by a name. Unlike other container types, no specific
restrictions are enforced on the contents name attribute.

**RSA**

This type of container is designed to hold references to only three different
secrets. These secrets are enforced by the their accompanied names: public_key,
private_key, and private_key_passphrase.

**Certificate**

This type of container is designed to hold a reference to a certificate and
optionally private_key, private_key_passphrase, and intermediates.


This table shows the possible response codes for this operation:



+------+-----------------------------------------------------------------------------+
| Code | Description                                                                 |
+======+=============================================================================+
| 201  | Successful creation of the container                                        |
+------+-----------------------------------------------------------------------------+
| 401  | Invalid X-Auth-Token or the token doesn't have permissions to this resource |
+------+-----------------------------------------------------------------------------+
| 403  | Forbidden.  The user has been authenticated, but is not authorized to       |
|      | create a container.  This can be based on the the user's role or the        |
|      | project's quota.                                                            |
+------+-----------------------------------------------------------------------------+

Request
""""""""""""""""


This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{tenantId}                |String *(Required)*      |This parameter specifies |
|                          |                         |the tenant ID of the     |
|                          |                         |client subscribing to    |
|                          |                         |the Barbican service     |
+--------------------------+-------------------------+-------------------------+



This table shows the body parameters for the request:


+-------------+--------+-----------------------------------------------------------+
| Name        | Type   | Description                                               |
+=============+========+===========================================================+
| name        | string | (optional) Human readable name for identifying your       |
|             |        | container                                                 |
+-------------+--------+-----------------------------------------------------------+
| type        | string | Type of container. Options: generic, rsa, certificate     |
+-------------+--------+-----------------------------------------------------------+
| secret_refs | list   | A list of dictionaries containing references to secrets   |
+-------------+--------+-----------------------------------------------------------+



**Example Create Container: JSON request**


.. code::

      curl -X POST -d \
        '{
            "type": "generic",
            "name": "container name",
            "secret_refs": [
                {
                    "name": "private_key",
                    "secret_ref": "https://{barbican_host}/v1/secrets/{secret_uuid}"
                }
            ]
        }'\
      https://endpointURL/v1/containers



Response
""""""""""""""""



**Example Create Container: JSON response**


.. code::

   {
       "container_ref": "https://{barbican_host}/v1/containers/{container_uuid"
   }
