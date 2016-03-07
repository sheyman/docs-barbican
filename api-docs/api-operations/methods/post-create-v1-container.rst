
.. _post-container:

Create a container
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /{version}/containers

Creates a container.

There are three different types of containers that can be created: generic,
rsa, and certificate.

**Generic**

This type of container holds any number of references to secrets. Each secret
reference is accompanied by a name. Unlike other container types, no specific
restrictions are enforced on the contents name attribute.

**RSA**

This type of container is designed to hold references to only three different
secrets. These secrets are enforced by the their accompanied names: public_key,
private_key, and private_key_passphrase.

**Certificate**

This type of container is designed to hold a reference to a certificate and
optionally private_key, private_key_passphrase, and intermediates.


This table shows the possible response codes for this operation:



+------+-----------------------------------------------------------------------------+
| Code | Description                                                                 |
+======+=============================================================================+
| 201  | Successful creation of the container                                        |
+------+-----------------------------------------------------------------------------+
| 401  | Invalid X-Auth-Token or the token doesn't have permissions to this resource |
+------+-----------------------------------------------------------------------------+
| 403  | Forbidden.  The user has been authenticated, but is not authorized to       |
|      | create a container.  This can be based on the the user's role or the        |
|      | project's quota.                                                            |
+------+-----------------------------------------------------------------------------+

Request
""""""""""""""""


There are no URL parameters for this request.


This table shows the body parameters for the request:


+-------------+--------+-----------------------------------------------------------+
| Name        | Type   | Description                                               |
+=============+========+===========================================================+
| name        | string | (optional) Human readable name for identifying your       |
|             |        | container                                                 |
+-------------+--------+-----------------------------------------------------------+
| type        | string | Type of container. Options: generic, rsa, certificate     |
+-------------+--------+-----------------------------------------------------------+
| secret_refs | list   | A list of dictionaries containing references to secrets   |
+-------------+--------+-----------------------------------------------------------+



**Example Create Container: JSON request**


.. code::

      curl -X POST -H 'X-Auth-Token {authToken} -d \
        '{
            "type": "generic",
            "name": "container name",
            "secret_refs": [
                {
                    "name": "private_key",
                    "secret_ref": "https://{endpoint}/v1/secrets/{secretID}"
                }
            ]
        }' https://{endpoint}/v1/containers

where:

- {endpoint} is the endpoint for the service
- {authToken} is the authentication token returned by the identity service
- {secretID} is the UUID for the secret to be added in the container.



Response
""""""""""""""""



**Example Create Container: JSON response**


.. code::

   {
       "container_ref": "https://{endpoint}/v1/containers/39dc45d8-4932-9ce7-8263-d9beda7410a0"
   }

The container ID is the UUID returned as the last part of the URL.  For this example, 
the container ID is 39dc45d8-4932-9ce7-8263-d9beda7410a0.