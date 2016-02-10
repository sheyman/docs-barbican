
.. _get-secret-information:

Get secret details
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /{version}/{tenantId}/secrets/{secret_id}

This method retrieves details about a secret.

This method retrieves the information for the specified secret. For the application/json accept type, only metadata about the secret is returned. If one of the 'content_types' accept types is specified instead, that portion of the secret will be decrypted and returned.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |Success                  |This status code is      |
|                          |                         |returned when the secret |
|                          |                         |has been successfully    |
|                          |                         |retrieved.               |
+--------------------------+-------------------------+-------------------------+
|404                       |Error                    |This error code is       |
|                          |                         |returned when the secret |
|                          |                         |metadata has been        |
|                          |                         |created, but the         |
|                          |                         |encrypted data for it    |
|                          |                         |has not yet been         |
|                          |                         |supplied, hence cannot   |
|                          |                         |be retrieved via a non   |
|                          |                         |'application/json' mime  |
|                          |                         |type                     |
+--------------------------+-------------------------+-------------------------+
|404                       |Error                    |This error code is       |
|                          |                         |returned when the        |
|                          |                         |supplied UUID doesn't    |
|                          |                         |match the secret in the  |
|                          |                         |datastore.               |
+--------------------------+-------------------------+-------------------------+
|406                       |Error                    |This error code is       |
|                          |                         |returned when the secret |
|                          |                         |data cannot be retrieved |
|                          |                         |in the requested Accept  |
|                          |                         |header mime-type         |
+--------------------------+-------------------------+-------------------------+


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
|{secret_id}               |String                   |This parameter specifies |
|                          |                         |the unique identifier of |
|                          |                         |a secret that has been   |
|                          |                         |stored.                  |
+--------------------------+-------------------------+-------------------------+





This operation does not accept a request body.




**Example Get Secret Information: JSON request**


.. code::

   curl -H 'Accept: application/json' \
   https://endpointURL/v1/12345/secrets/secretID/888b29a4-c7cf-49d0-bfdf-bd9e6f26d718





Response
""""""""""""""""


**Example Get Secret Information: JSON response**


.. code::

   {
       "status": "ACTIVE",
       "secret_ref": "https://endpointURL/v1/12345/secrets/513ed616-2686-4ce5-a96c-fea785fe527b",
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
