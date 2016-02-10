
.. _delete-container:

Delete a container
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    DELETE /v1/containers/{uuid}

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

      DELETE /v1/containers/{container_uuid}
      Headers:
      X-Project-Id: {project_id}

Response
""""""""""""""""

The operation does not return a response body.
