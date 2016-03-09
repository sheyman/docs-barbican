
.. _get-containers:

Get Containers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /{version}/containers

Returns a list of a project's containers.

Returned containers will be ordered by creation date; oldest to newest.

This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |This status code is      |
|                          |                         |returned when the        |
|                          |                         |containers have been     |
|                          |                         |successfully retrieved   |
|                          |                         |for the tenant.          |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |This status code is      |
|                          |                         |returned when the        |
|                          |                         |user was not succesfully |
|                          |                         |authenticated.           |
+--------------------------+-------------------------+-------------------------+
|403                       |Forbidden                |This status code is      |
|                          |                         |returned when the        |
|                          |                         |user does not have the   |
|                          |                         |correct RBAC role(s).    |
+--------------------------+-------------------------+-------------------------+


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

    curl -H 'Accept: application/json' -H 'X-Auth-Token:{authToken}'\
    https://{endpoint}/v1/containers?offset={offset}&limit={limit}

where:

- {endpoint} is the endpoint for the service
- {authToken} is the authentication token returned by the identity service
- {offset} is the offset into the list of containers where the returned list will start
- {limit} is the max number of containers to return in the list


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
                "container_ref": "https://iad.keep.api.rackspacecloud.com/v1/containers/6ad67bc0-17fd-45ce-b84a-a9be44fe069b",
                "created": "2015-03-26T21:10:45.417835",
                "name": "container name",
                "secret_refs": [
                    {
                        "name": "private_key",
                        "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/485950f0-37a5-4ba4-b1d6-413f79b849ef"
                    }
                ],
                "status": "ACTIVE",
                "type": "generic",
                "updated": "2015-03-26T21:10:45.417835"
            }
        ],
        "total": 1
      }

where:

- the container ID is 6ad67bc0-17fd-45ce-b84a-a9be44fe069b
- the secret ID is 485950f0-37a5-4ba4-b1d6-413f79b849ef
- the endpoint is iad.keep.api.rackspacecloud.com
