
.. _get-secret-information:

Get secret metadata
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /{version}/secrets/{secret_id}

This method retrieves the metadata for the specified secret.

This table shows possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |Success                  |This status code is      |
|                          |                         |returned when the secret |
|                          |                         |metadata has been        |
|                          |                         |successfully retrieved.  |
+--------------------------+-------------------------+-------------------------+
|404                       |Not Found                |This error code is       |
|                          |                         |returned when the secret |
|                          |                         |id is invalid.           |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""

This operation does not accept a request body.



**Example Get Secret Metadata: JSON request**


.. code::

   curl -H 'Accept: application/json' -H 'X-Auth-Token: $AUTH-TOKEN'\
   $ENDPOINT/v1/secrets/secretID/{secretID}


where:

- {endpoint} is the endpoint for the service
- $AUTH-TOKEN is the authentication token returned by the identity service
- {secretID} is the UUID for the secret to be deleted.


Response
""""""""""""""""


**Example Get Secret Information: JSON response**


.. code::

   {
       "status": "ACTIVE",
       "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/485950f0-37a5-4ba4-b1d6-413f79b849ef",
       "updated": "2014-05-02T06:29:25.415271",
       "name": "AES key",
       "algorithm": "aes",
       "created": "2014-05-02T06:29:25.415261",
       "content_types": {
           "default": "application/octet-stream"
       },
       "mode": "cbc",
       "bit_length": 256,
       "expiration": "2014-05-28T19:14:44.180394"
   }


where:

- the secret ID is 485950f0-37a5-4ba4-b1d6-413f79b849ef
- the endpoint is iad.keep.api.rackspacecloud.com