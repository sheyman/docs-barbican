
.. _get-container-information:

Get Container Information
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /v1/containers/{container_uuid}

This method retrieves information about a specified container.

This method retrieves information for the specified order including a link to the secret that was stored as a result of the order (if available).


This table shows the possible response codes for this operation:


++------+-----------------------------------------------------------------------------+
| Code | Description                                                                 |
+======+=============================================================================+
| 200  | Successful Request                                                          |
+------+-----------------------------------------------------------------------------+
| 401  | Invalid X-Auth-Token or the token doesn't have permissions to this resource |
+------+-----------------------------------------------------------------------------+
| 404  | Container not found or unavailable                                          |
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
|                          |                         |the Cloud Keep service.  |
+--------------------------+-------------------------+-------------------------+
|{container_uuid}          |String *(Required)*      |This parameter specifies |
|                          |                         |the unique identifier of |
|                          |                         |a container that has     |
|                          |                         |been stored.             |
+--------------------------+-------------------------+-------------------------+



This operation does not accept a request body.



**Example Get Container Information: JSON request**


.. code::

      curl -H 'Accept: application/json' -H 'X-Project-Id:12345'\
      https://endpointURL/v1/containers/{container_uuid}



Response
""""""""""""""""


**Example Get Container Information: JSON response**


.. code::

    {
        "type": "generic",
        "status": "ACTIVE",
        "name": "container name",
        "consumers": [],
        "container_ref": "https://{barbican_host}/v1/containers/{uuid}",
        "secret_refs": [
          {
              "name": "private_key",
              "secret_ref": "https://{barbican_host}/v1/secrets/{uuid}"
          }
        ],
        "created": "2015-03-26T21:10:45.417835",
        "updated": "2015-03-26T21:10:45.417835"
    }
