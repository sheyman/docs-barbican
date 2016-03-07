
.. _post-consumers:

Create a consumer
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /{version}/containers/{container_id}/consumers


Creates a consumer for the specified container.

This table shows the possible response codes for this operation:

+------+-----------------------------------------------------------------------------+
| Code | Description                                                                 |
+======+=============================================================================+
| 201  | Successful creation of the consumer                                         |
+------+-----------------------------------------------------------------------------+
| 401  | Invalid X-Auth-Token or the token doesn't have permissions to this resource |
+------+-----------------------------------------------------------------------------+
| 403  | Forbidden.  The user has been authenticated, but is not authorized to       |
|      | create a consumer.  This can be based on the the user's role or the         |
|      | project's quota.                                                            |
+------+-----------------------------------------------------------------------------+


Request
""""""""""""""""



There are no URL parameters for this request.


This table shows the body parameters for the request:



+----------------------------+---------+----------------------------------------------+------------+
| Parameter name             | Type    | Description                                  | Default    |
+============================+=========+==============================================+============+
| name                       | string  | The name of the consumer set by the user.    | None       |
+----------------------------+---------+----------------------------------------------+------------+
| url                        | string  | The url for the user or service using the    | None       |
|                            |         | container.                                   |            |
+----------------------------+---------+----------------------------------------------+------------+


**Example Create consumer: JSON request**


.. code::

      curl -X POST -H 'X-Auth-Token {authToken} -H 'Content-Type: application/json' \
        -d '{
            "name": "your consumer name",
            "url": "{consumerURL}"
        }' https://{endpoint}/v1/containers/{containerID}/consumers

where:

- {endpoint} is the endpoint for the service
- {authToken} is the authentication token returned by the identity service
- {containerID} is the UUID for the container
- {consumerURL} is the URL for the consumer


Response
""""""""""""""""

**Example Create Consumer: JSON response**


.. code::

    {
        "status": "ACTIVE",
        "updated": "2015-10-15T17:56:18.626724",
        "name": "your container name",
        "consumers": [
            {
                "URL": "{consumerURL}",
                "name": "your consumer name"
            }
    }
