.. _gsg-retrieve-a-secret:

Retrieve a secret
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After you have created and stored a secret, you can submit a **GET**
request to retrieve either the secret metadata or the actual decrypted
secret, depending on the URL that is used in the
**GET** request.

A **GET** to the /v1/secrets/$SECRET_ID resource will return only the secret metadata.

A **GET** to the /v1/secrets/$SECRET_ID/payload resource will return the decrypted secret itself. 

The following example shows how to retrieve secret metadata by
submitting a **GET** request against the endpoint URL with the tenant ID
and secret ID specified.

.. code::

      curl -H 'X-Auth-Token: '$AUTH_TOKEN $API_ENDPOINT/v1/secrets/$SECRET_ID | python -m json.tool

If the call is successful, you receive a response like the following (assuming your API_ENDPOINT
is https://iad.keep.api.rackspacecloud.com:

.. code::

    {
        "algorithm": "aes",
        "bit_length": 256,
        "content_types": {
            "default": "application/octet-stream"
        },
        "created": "2016-02-29T19:25:31.993225",
        "creator_id": "9a756651fa1046c983d8afaefd4f0c71",
        "expiration": "2020-02-28T19:14:44.180394",
        "mode": "cbc",
        "name": "AES key",
        "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/578391c7-92fa-484f-8546-3562b170e5",
        "secret_type": "opaque",
        "status": "ACTIVE",
        "updated": "2016-02-29T19:25:31.999733"
    }

The following example shows how to retrieve the secret payload by
submitting a **GET** request against the endpoint URL with the tenant ID
and secret ID specified.

.. code::

      curl -H 'X-Auth-Token: '$AUTH_TOKEN $API_ENDPOINT/v1/secrets/$SECRET_ID/payload

If the call is successful, you receive a response containing the decrypted secret.

..  note::

      Note
      The /payload shown above on the URL tells the API to return the secret's payload.  If you omit /payload then you will get just the secret metadata.

