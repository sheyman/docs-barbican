.. _gsg-retrieve-a-secret:

Retrieve a secret
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After you have created and stored a secret, you can submit a **GET**
request to retrieve either the secret metadata or the actual decrypted
secret, depending on the URL that is used in the
**GET** request.

- To retrieve only the secret metadata, submit the request to the ``/v1/secrets/$SECRET_ID`` resource.
- To retrieve the decrypted secret, submit the request to the ``/v1/secrets/$SECRET_ID/payload`` resource. 

**Example: Retrieve secret metadata request**

The following example retrieves the secret metadata by
submitting a **GET** request against the endpoint URL with the secret ID specified.

.. code::

      curl -X GET $API_ENDPOINT/v1/secrets/$SECRET_ID  \
           -H "X-Auth-Token: $AUTH_TOKEN" | python -m json.tool
     

If the call is successful, the response looks like the following example, assuming that your API_ENDPOINT
is ``https://iad.keep.api.rackspacecloud.com``:

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

**Example: Retrieve decrypted secret request**

The following example shows how to retrieve the secret payload by
submitting a **GET** request against the endpoint URL with the secret ID specified.

.. code::

      curl -X GET $API_ENDPOINT/v1/secrets/$SECRET_ID/payload \
           -H "X-Auth-Token: $AUTH_TOKEN"

If the call is successful, you receive a response containing the decrypted secret.


