
.. _delete-secret:

Delete a secret
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    DELETE /{version}/secrets/{secret_id}



Deletes the specified secret.

This table shows the possible response codes for this operation:


+------+-----------------------------------------------------------------------------+
| Code | Description                                                                 |
+======+=============================================================================+
| 204  | Successful request                                                          |
+------+-----------------------------------------------------------------------------+
| 401  | Invalid X-Auth-Token or the token doesn't have permissions to this resource |
+------+-----------------------------------------------------------------------------+
| 404  | Secret not found                                                            |
+------+-----------------------------------------------------------------------------+


Request
""""""""""""""""

This operation doesn't take a request body.

**Example Delete secret: JSON request**


.. code::

   curl -X DELETE -H 'X-Auth-Token: {authToken}' \
        https://{endpoint}/v1/secrets/{secretID}

where:

- {endpoint} is the endpoint for the service
- {authToken} is the authentication token returned by the identity service
- {secretID} is the UUID for the secret to be deleted.

Response
""""""""""""""""

This operation will return an HTTP 204 for a successful delete.  It does not return a response body.
