
.. _delete-consumer:

Delete a consumer
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    DELETE /{version}/{container_ref}/consumers/{consumer_id}


Deletes the specified consumer for the specified container.


+------+-----------------------------------------------------------------------------+
| Code | Description                                                                 |
+======+=============================================================================+
| 204  | Successful request                                                          |
+------+-----------------------------------------------------------------------------+
| 401  | Invalid X-Auth-Token or the token doesn't have permissions to this resource |
+------+-----------------------------------------------------------------------------+
| 404  | Not Found                                                                   |
+------+-----------------------------------------------------------------------------+


Request
""""""""""""""""

This operation does not accept a request body.

**Example Delete consumer: JSON request**


.. code::

   curl -X DELETE -H 'X-Auth-Token: {authToken}' \
        https://{endpoint}/v1/containers/{containerID}/consumers/{consumerID}

where

- {endpoint} is the endpoint for the service
- {authToken} is the authentication token returned by the identity service
- {containerID} is the UUID for the container
- {consumerID} is the UUID for the consumer to be deleted from the container

Response
""""""""""""""""

This operation will return an HTTP 204 for a successful delete.  It does not return a response body.
