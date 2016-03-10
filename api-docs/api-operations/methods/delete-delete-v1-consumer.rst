
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

The following table shows the URI parameters for the request:

+----------------------------+---------+----------------------------------------------+------------+
| Parameter name             | Type    | Description                                  | Default    |
+============================+=========+==============================================+============+
|containerID                 | string  | The UUID for the container                   | None       |
+----------------------------+---------+----------------------------------------------+------------+
|consumerID                  | string  | The UUID for the consumer                    | None       |
+----------------------------+---------+----------------------------------------------+------------+

**Example Delete consumer: JSON request**

.. code::

   curl -X DELETE -H 'X-Auth-Token: $AUTH-TOKEN' \
        $ENDPOINT/v1/containers/{containerID}/consumers/{consumerID}


Response
""""""""""""""""

This operation will return an HTTP 204 for a successful delete.  It does not return a response body.
