.. _gsg-retrieve-list-of-stored-secrets:

Retrieve a list of stored secrets
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


You can retrieve a list of secrets that are associated with a given
tenant by typing the following command:

.. code::

    curl -H 'Accept: application/json' https://endpointURL/v1/tenantID/secrets

If the call is successful, you receive a response like the following
one:

.. code::

    {
        "secrets": [
            {
                "status": "ACTIVE",
                "secret_ref": "https://endpointURL/v1/tenantID/secrets/9150d09b-7791-4c2a-90cc-1592e2ff67ac",
                "updated": "2014-03-19T22:39:55.136579",
                "name": "aes_key",
                "algorithm": "aes",
                "created": "2014-03-19T22:39:55.136567",
                "content_types": {
                    "default": "application/octet-stream"
                },
                "mode": "CDC",
                "bit_length": 256,
                "expiration": null
            },
            {
                "status": "ACTIVE",
                "secret_ref": "https://endpointURL/v1/tenantID/secrets/2e21bffa-2b81-432a-9bcb-2533593bcd34",
                "updated": "2014-03-19T22:39:56.018075",
                "name": "aes_key",
                "algorithm": "aes",
                "created": "2014-03-19T22:39:56.018061",
                "content_types": {
                    "default": "application/octet-stream"
                },
                "mode": "CDC",
                "bit_length": 256,
                "expiration": null
            },
            {
                "status": "ACTIVE",
                "secret_ref": "https://endpointURL/v1/tenantID/secrets/54bf3411-0765-467c-ba76-ba96c527e990",
                "updated": "2014-03-19T22:40:17.100402",
                "name": "secretname",
                "algorithm": "aes",
                "created": "2014-03-19T22:40:17.100389",
                "content_types": {
                    "default": "application/octet-stream"
                },
                "mode": "cbc",
                "bit_length": 256,
                "expiration": null
            }
        ],
        "total": 84,
        "next": "https://endpointURL/v1/tenantID/secrets?limit=10&offset=10"
    }
