
.. _delete-container:

Delete a container
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    DELETE /{version}/containers/{container_id}

Deletes a container.

This table shows the possible response codes for this operation:

+------+-----------------------------------------------------------------------------+
| Code | Description                                                                 |
+======+=============================================================================+
| 204  | Successful deletion of a container                                          |
+------+-----------------------------------------------------------------------------+
| 401  | Invalid X-Auth-Token or the token doesn't have permissions to this resource |
+------+-----------------------------------------------------------------------------+
| 404  | Container not found or unavailable                                          |
+------+-----------------------------------------------------------------------------+



Request
""""""""""""""""

This operation does not accept a request body.

**Example Delete container: JSON request**


.. code::

   curl -X DELETE -H 'X-Auth-Token: {authToken}' \
        https://{endpoint}/v1/containers/{containerID}

where

- {endpoint} is the endpoint for the service
- {authToken} is the authentication token returned by the identity service
- {containerID} is the UUID for the container to be deleted.

Response
""""""""""""""""

This operation will return an HTTP 204 for a successful delete.  It does not return a response body.
