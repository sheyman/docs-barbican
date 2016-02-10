
.. _get-containers:

Get Containers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /{version}/{tenantId}/containers

Lists a project's containers.

Returned containers will be ordered by creation date; oldest to newest.

This table shows the possible response codes for this operation:



+------+-----------------------------------------------------------------------------+
| Code | Description                                                                 |
+======+=============================================================================+
| 200  | Successful Request                                                          |
+------+-----------------------------------------------------------------------------+
| 401  | Invalid X-Auth-Token or the token doesn't have permissions to this resource |
+------+-----------------------------------------------------------------------------+


Request
""""""""""""""""


This table shows the URI parameters for the request:

+--------+---------+------------------------------------------------------------+
| Name   | Type    | Description                                                |
+========+=========+============================================================+
| offset | integer | The starting index within the total list of the containers |
|        |         | that you would like to retrieve.                           |
+--------+---------+------------------------------------------------------------+
| limit  | integer | The maximum number of containers to return (up to 100).    |
|        |         | The default limit is 10.                                   |
+--------+---------+------------------------------------------------------------+


This operation does not accept a request body.


**Example Get Containers: JSON request**


.. code::

    curl -H 'Accept: application/json' -H 'X-Project-Id:12345'\
    https://endpointURL/v1/containers


Response
""""""""""""""""

This table shows the response parameters for the request:

+------------+---------+--------------------------------------------------------+
| Name       | Type    | Description                                            |
+============+=========+========================================================+
| containers | list    | Contains a list of dictionaries filled with container  |
|            |         | data                                                   |
+------------+---------+--------------------------------------------------------+
| total      | integer | The total number of containers available to the user   |
+------------+---------+--------------------------------------------------------+
| next       | string  | A HATEOAS url to retrieve the next set of containers   |
|            |         | based on the offset and limit parameters. This         |
|            |         | attribute is only available when the total number of   |
|            |         | containers is greater than offset and limit parameter  |
|            |         | combined.                                              |
+------------+---------+--------------------------------------------------------+
| previous   | string  | A HATEOAS url to retrieve the previous set of          |
|            |         | containers based on the offset and limit parameters.   |
|            |         | This attribute is only available when the request      |
|            |         | offset is greater than 0.                              |
+------------+---------+--------------------------------------------------------+


**Example Get Containers: JSON response**


.. code::

      {
        "containers": [
            {
                "consumers": [],
                "container_ref": "https://{barbican_host}/v1/containers/{uuid}",
                "created": "2015-03-26T21:10:45.417835",
                "name": "container name",
                "secret_refs": [
                    {
                        "name": "private_key",
                        "secret_ref": "https://{barbican_host}/v1/secrets/{uuid}"
                    }
                ],
                "status": "ACTIVE",
                "type": "generic",
                "updated": "2015-03-26T21:10:45.417835"
            }
        ],
        "total": 1
      }
