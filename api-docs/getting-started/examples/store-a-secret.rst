
.. _gsg-store-a-secret:

Store a secret
~~~~~~~~~~~~~~~~~~~~


You can store a secret by submitting a **POST** request against the
secrets resource and include the secret in the *``payload``* parameter.
You specify the secret payload type in the ``payload_content_type``
parameter:

-  For texts-based secrets, set the ``payload_content_type`` parameter
   to ``text/plain``.

-  For binary secrets, set the ``payload_content_type`` parameter to
   ``application/octet-stream``.

..  note::

      Note
      Submitting a **POST** request creates secret metadata. If the payload is
      provided with the **POST** request, then it is encrypted and stored, and
      then linked with this metadata. If no payload is included with the
      **POST** request, it must be provided with a subsequent **PUT** request.
      The secret resource encrypts and stores client-provided secret
      information and metadata. In contrast, the orders resource generats
      actual secret information on behalf of clients.

      The following example shows how to store a secret in the format of an
      AES key by submitting a **POST** request wth the base64-encoded secret
      payload specified against the secrets resource.

.. code::

      curl -X POST -H 'Content-Type: application/json' -H 'Accept: application/json' -d\
        '{
            "name": "AES key",
            "expiration": "2014-02-28T19:14:44.180394",
            "algorithm": "aes",
            "bit_length": 256,
            "mode": "cbc",
            "payload": "gF6+lLoF3ohA9aPRpt+6bQ==",
            "payload_content_type": "application/octet-stream",
            "payload_content_encoding": "base64"
          }'\
              http://<endpointURL>/v1/<tenantId>/secrets

If the request is successful, you will receive a response like the
following:

.. code::

        "secret_ref": "https://endpointURL/v1/tenantID/secrets/a8957047-16c6-4b05-ac57-8621edd0e9ee"

The example above shows the secretId, which will be returned in a
successful response.

..  note::


      Note
      You can also store a secret by first submitting a **POST** request
      without specifying the secret payload and then submitting a subsequent
      **PUT** request with the payload. This storage mode enables you to
      upload a a binary file to the Barbican database directly for encrypted
      storage. For more information, read Two-step call flow for binary
      secrets.
