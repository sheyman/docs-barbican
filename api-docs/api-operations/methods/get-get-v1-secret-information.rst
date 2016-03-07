
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

   curl -H 'Accept: application/json' -H 'X-Auth-Token: {authToken}'\
   https://{endpoint}/v1/secrets/secretID/{secretID}


where:

- {endpoint} is the endpoint for the service
- {authToken} is the authentication token returned by the identity service
- {secretID} is the UUID for the secret to be deleted.


Response
""""""""""""""""


**Example Get Secret Information: JSON response**


.. code::

   {
       "status": "ACTIVE",
       "secret_ref": "https://{endpoint}/v1/secrets/888b29a4-c7cf-49d0-bfdf-bd9e6f26d718",
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
