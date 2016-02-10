.. _gsg-retrieve-a-secret:

Retrieve a secret
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After you have created and stored a secret, you can submit a **GET**
request to retrieve either the secret metadata or the actual decrypted
secret, depending on the ``Accept`` header that is provided in the
**GET** request. For more information on different possibilities and
combinations for setting the ``Accept`` header, read Examples of secret
combinations.

The following example shows how to retrieve secret metadata by
submitting a **GET** request against the endpoint URL with the tenantID
and secretID parameters specified and the ``Accept`` header set to
``application/json``.

.. code::

      curl -H 'Accept: application/json' https://endpointURL/v1/tenantID/secrets/secretID

If the call is successful, you receive a response like the following:

.. code::

      curl -X POST -H 'Content-Type: application/json' -H 'Accept: application/json' -d\
        '{
            "name": "AES key",
            "expiration": "2014-02-28T19:14:44.180394",
            "algorithm": "aes",
            "bit_length": 256,
            "mode": "cbc"
          }'\
          http://<endpointURL>/v1/<tenantId>/secrets


.. Important::

      Important
      To retrieve the decrypted secret information, set the ``Accept`` header
      to either ``application/octet-stream`` for binary secrets or to
      ``text/plain`` for text-based secrets.
