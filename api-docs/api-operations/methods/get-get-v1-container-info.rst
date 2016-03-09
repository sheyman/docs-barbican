
.. _get-container-information:

Get Container Information
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /{version}/containers/{container_id}

This method retrieves information about a specified container.


This table shows the possible response codes for this operation:


+------+-----------------------------------------------------------------------------+
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
|{container_id}            |String *(Required)*      |This parameter specifies |
|                          |                         |the unique identifier of |
|                          |                         |a container that has     |
|                          |                         |been stored.             |
+--------------------------+-------------------------+-------------------------+



This operation does not accept a request body.



**Example Get Container Information: JSON request**


.. code::

      curl -H 'Accept: application/json' -H 'X-Auth-Token:{authToken}' \
         https://{endpoint}/v1/containers/{containerID}


where:

- {endpoint} is the endpoint for the service
- {authToken} is the authentication token returned by the identity service
- {containerID} is the ID of the container for which we want the information


Response
""""""""""""""""


**Example Get Container Information: JSON response**


.. code::

    {
        "type": "generic",
        "status": "ACTIVE",
        "name": "container name",
        "consumers": [],
        "container_ref": "https://iad.keep.api.rackspacecloud.com/v1/containers/6ad67bc0-17fd-45ce-b84a-a9be44fe069b",
        "secret_refs": [
          {
              "name": "private_key",
              "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/485950f0-37a5-4ba4-b1d6-413f79b849ef"
          }
        ],
        "created": "2015-03-26T21:10:45.417835",
        "updated": "2015-03-26T21:10:45.417835"
    }


where:

- the container ID is 6ad67bc0-17fd-45ce-b84a-a9be44fe069b
- the secret ID is 485950f0-37a5-4ba4-b1d6-413f79b849ef
- the endpoint is iad.keep.api.rackspacecloud.com