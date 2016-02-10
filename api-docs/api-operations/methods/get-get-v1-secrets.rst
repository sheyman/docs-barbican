
.. _get-secrets:

Get Secrets
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /{version}/{tenantId}/secrets

This method retrieves all secrets for a given tenant.

This method lists all the secrets for a tenant.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |Error                    |This status code is      |
|                          |                         |returned when the        |
|                          |                         |secrets have been        |
|                          |                         |successfully retrieved   |
|                          |                         |for the tenant.          |
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



This operation does not accept a request body.


**Example Get Secrets: JSON request**


.. code::

   curl -H 'Accept: application/json' -H 'X-Project-Id: 12345' \
   https://endpointURL/v1/secrets





Response
""""""""""""""""


**Example Get Secrets: JSON response**


.. code::

   {
       "secrets": [
           {
               "status": "ACTIVE",
               "secret_ref": "http://endpointURL/v1/secrets/15108db8-4505-4c5b-96b9-a9838951f28f",
               "updated": "2014-08-25T20:43:01.510569",
               "name": "secretname",
               "algorithm": "aes",
               "created": "2014-08-25T20:43:01.421625",
               "content_types": {
                   "default": "application/octet-stream"
               },
               "mode": "cbc",
               "bit_length": 256,
               "expiration": null
           },
           {
               "status": "ACTIVE",
               "secret_ref": "http://endpointURL/v1/secrets/f74a51d2-99a8-423a-8cea-2bf10b263584",
               "updated": "2014-08-25T21:18:35.821340",
               "name": "secretname",
               "algorithm": "aes",
               "created": "2014-08-25T21:18:35.719952",
               "content_types": {
                   "default": "application/octet-stream"
               },
               "mode": "cbc",
               "bit_length": 256,
               "expiration": null
           }
       ],
       "total": 4,
       "next": "http://endpointURL/v1/secrets?limit=2&offset=3",
       "previous": "http://endpointURL/v1/secrets?limit=2&offset=0"
   }
