.. _gsg-retrieve-list-of-stored-secrets:

Retrieve a list of stored secrets
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


You can retrieve a list of secrets that are associated with your
tenant by issing the following command:

.. code::

    curl -H 'X-Auth-Token: '$AUTH_TOKEN $API_ENDPOINT/v1/secrets?limit=5\&offset=0 | python -m json.tool

..  note::

      Using URL parameters, you can control the number of secrets to return (limit) as well as a starting point (offset).  If you omit these URL parameters, the defaults are limit=10 and offset=0.  The returned data will contain a "next" and/or "previous" field as you issue subsequent **GET** calls with different limits and offsets.  These fields can be used to help you nagivate through your entire list of secrets.


If the call is successful, you receive a response like the following
one:

.. code::

    {
    "next": "https://iad.keep.api.rackspacecloud.com/v1/secrets?limit=5&offset=5",
    "secrets": [
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
        },
        {
            "algorithm": "aes",
            "bit_length": 256,
            "content_types": {
                "default": "application/octet-stream"
            },
            "created": "2016-02-29T19:23:44.974085",
            "creator_id": "9a756651fa1046c983d8afaefd4f0c71",
            "expiration": "2020-02-28T19:14:44.180394",
            "mode": "cbc",
            "name": "AES key",
            "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/94f88434-512c-4b4b-be3e-9469fc6824e2",
            "secret_type": "opaque",
            "status": "ACTIVE",
            "updated": "2016-02-29T19:23:44.981439"
        },
        {
            "algorithm": "aes",
            "bit_length": 256,
            "content_types": {
                "default": "application/octet-stream"
            },
            "created": "2016-02-29T19:18:15.639569",
            "creator_id": "9a756651fa1046c983d8afaefd4f0c71",
            "expiration": "2020-02-28T19:14:44.180394",
            "mode": "cbc",
            "name": "AES key",
            "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/98bccb6e-67c6-87a9-b7a4-98198b4f1732",
            "secret_type": "opaque",
            "status": "ACTIVE",
            "updated": "2016-02-29T19:18:15.648516"
        },
        {
            "algorithm": "aes",
            "bit_length": 256,
            "content_types": {
                "default": "application/octet-stream"
            },
            "created": "2016-02-29T19:13:37.888706",
            "creator_id": "9a756651fa1046c983d8afaefd4f0c71",
            "expiration": "2018-02-28T19:14:44.180394",
            "mode": "cbc",
            "name": "AES key",
            "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/ba87c04f-797c-4f69-8fb6-d01db61d9573",
            "secret_type": "opaque",
            "status": "ACTIVE",
            "updated": "2016-02-29T19:13:37.896416"
        },
        {
            "algorithm": "aes",
            "bit_length": 256,
            "content_types": {
                "default": "application/octet-stream"
            },
            "created": "2016-02-29T15:54:34.474305",
            "creator_id": "9a756651fa1046c983d8afaefd4f0c71",
            "expiration": "2018-02-28T19:14:44.180394",
            "mode": "cbc",
            "name": "AES key",
            "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/19f7f7aa-817c-49cc-b252-441df7b44a4c",
            "secret_type": "opaque",
            "status": "ACTIVE",
            "updated": "2016-02-29T15:54:34.485707"
        }
    ],
    "total": 23
    }
