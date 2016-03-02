.. _gsg-retrieve-list-of-stored-secrets:

Retrieve a list of stored secrets
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Perform a **GET** request on the secrets resource to retrieve a list of 
:ref:`secrets <secrets-concept>` that are associated with your tenant.

By default, the API request returns the first 11 secrets associated with the tenant. You 
can use the *limit* and *offset* request parameters to limit the number of secrets 
returned in a single request and to set the starting point for the list. 

The following example specifies ``limit`` and ``offset`` values to return five secrets, starting 
with the first. 


**Example: Retrieve list of secrets request**

.. code::
    
    curl -X GET $API_ENDPOINT/v1/secrets?limit=5\&offset=0 \
         -H "Accept: application/json" \
         -H "X-Auth-Token: $AUTH_TOKEN" \
         -H "Content-Type: application/json" \
         | python -m json.tool



If the operation is successful, the response returns a list of secrets as shown in the 
following example. 

.. note:: 
    
    If additional secrets have been stored, the returned data contains 
    ``next`` and ``previous`` links so that you can page through the data. 



**Example:  Retrieve list of secrets response**

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


