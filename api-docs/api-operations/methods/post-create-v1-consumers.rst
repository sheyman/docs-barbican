
.. _post-consumers:

Create a consumer
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

  POST {container_ref}/consumers


Creates a consumer.

This table shows the possible response codes for this operation:

+------+-----------------------------------------------------------------------------+
| Code | Description                                                                 |
+======+=============================================================================+
| 200  | OK                                                                          |
+------+-----------------------------------------------------------------------------+
| 400  | Bad Request                                                                 |
+------+-----------------------------------------------------------------------------+
| 401  | Invalid X-Auth-Token or the token doesn't have permissions to this resource |
+------+-----------------------------------------------------------------------------+
| 403  | Forbidden.  The user has been authenticated, but is not authorized to       |
|      | create a consumer. This can be based on the the user's role or the          |
|      | project's quota.                                                            |
+------+-----------------------------------------------------------------------------+


Request
""""""""""""""""


The following table shows the URI parameters for the request:


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

      POST {container_ref}/consumers
      Headers:
      X-Project-Id: {project_id}

      Content:
      {
        "name": "ConsumerName",
        "url": "ConsumerURL"
      }

Response
""""""""""""""""

**Example Create Consumer: JSON response**


.. code::

    200 OK

    {
        "status": "ACTIVE",
        "updated": "2015-10-15T17:56:18.626724",
        "name": "container name",
        "consumers": [
            {
                "URL": "consumerURL",
                "name": "consumername"
            }
    ],
      "created": "2015-10-15T17:55:44.380002",
      "container_ref": "http://localhost:9311/v1/containers/74bbd3fd-9ba8-42ee-b87e-2eecf10e47b9",
      "creator_id": "b17c815d80f946ea8505c34347a2aeba",
      "secret_refs": [
          {
            "secret_ref": "http://localhost:9311/v1/secrets/b61613fc-be53-4696-ac01-c3a789e87973",
            "name": "private_key"
          }
    ],
      "type": "generic"
    }
