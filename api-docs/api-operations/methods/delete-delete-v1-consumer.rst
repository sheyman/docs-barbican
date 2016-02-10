
.. _delete-consumer:

Delete a consumer
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    DELETE {container_ref}/consumers


Deletes a consumer.


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

    DELETE {container_ref}/consumers
    Headers: X-Project-Id: {project_id}



Response
""""""""""""""""

This operation does not return a response body.
