
.. _delete-secret:

Delete a secret
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    DELETE /v1/secrets/{uuid}



Deletes a secret by UUId.

This table shows the possible response codes for this operation:


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

This operation doesn't take a request body.

**Example Delete secret: JSON request**


.. code::

   DELETE /v1/secrets/{uuid}
   Headers: X-Project-Id: {project_id}

Response
""""""""""""""""

This operation doesn't return a response body.
