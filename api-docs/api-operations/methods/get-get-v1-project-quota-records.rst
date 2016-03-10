
.. _get-project-quota-records:

Get Project quota records
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

  GET /{version}/project-quotas

Gets a list of configured project quota records.  Paging is supported using the
optional parameters offset and limit.


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

There are no URL parameters for this operation.


This table shows the body parameters for the request:


+--------+---------+----------------------------------------------------------------+
| Name   | Type    | Description                                                    |
+========+=========+================================================================+
| offset | integer | The starting index within the total list of the project        |
|        |         | quotas that you would like to receive.                         |
+--------+---------+----------------------------------------------------------------+
| limit  | integer | The maximum number of records to return.                       |
+--------+---------+----------------------------------------------------------------+


**Example Get project quotas: JSON request**


.. code::

   curl -H 'Accept: application/json' -H 'X-Auth-Token:{authToken}'\
      https://{endpoint}/v1/project-quotas/?offset={offset}&limit={limit}

where:

- {endpoint} is the endpoint for the service
- {authToken} is the authentication token returned by the identity service
- {offset} is the offset into the list of project quotas
- {limit} is the maximum number of project quotas to return


Response
""""""""""""""""

This table shows the response parameters for the request.


+----------------+---------+--------------------------------------------------------------+
| Name           | Type    | Description                                                  |
+================+=========+==============================================================+
| project-id     | string  | The UUID of a project with configured quota information.     |
+----------------+---------+--------------------------------------------------------------+
| project-quotas | dict    | Contains a dictionary with project quota information.        |
+----------------+---------+--------------------------------------------------------------+
| secrets        | integer | Contains the effective quota value of the current project    |
|                |         | for the secret resource.                                     |
+----------------+---------+--------------------------------------------------------------+
| orders         | integer | Reserved for future use.                                     |
+----------------+---------+--------------------------------------------------------------+
| containers     | integer | Contains the effective quota value of the current project    |
|                |         | for the containers resource.                                 |
+----------------+---------+--------------------------------------------------------------+
| consumers      | integer | Contains the effective quota value of the current project    |
|                |         | for the consumers resource.                                  |
+----------------+---------+--------------------------------------------------------------+
| cas            | integer | Reserved for future use.                                     |
+----------------+---------+--------------------------------------------------------------+
| total          | integer | The total number of configured project quotas records.       |
+----------------+---------+--------------------------------------------------------------+
| next           | string  | A HATEOAS url to retrieve the next set of quotas based on    |
|                |         | the offset and limit parameters. This attribute is only      |
|                |         | available when the total number of secrets is greater than   |
|                |         | offset and limit parameter combined.                         |
+----------------+---------+--------------------------------------------------------------+
| previous       | string  | A HATEOAS url to retrieve the previous set of quotas based   |
|                |         | on the offset and limit parameters. This attribute is only   |
|                |         | available when the request offset is greater than 0.         |
+----------------+---------+--------------------------------------------------------------+


Configured project quota values are interpreted as follows:

+-------+-----------------------------------------------------------------------------+
| Value | Description                                                                 |
+=======+=============================================================================+
|  -1   | A negative value indicates the resource is unconstrained by a quota.        |
+-------+-----------------------------------------------------------------------------+
|   0   | A zero value indicates that the resource is disabled.                       |
+-------+-----------------------------------------------------------------------------+
| int   | A positive value indicates the maximum number of that resource that can be  |
|       | created for the current project.                                            |
+-------+-----------------------------------------------------------------------------+
| null  | A null value indicates that the default quota value for the resource        |
|       | will be used as the quota for this resource in the current project.         |
+-------+-----------------------------------------------------------------------------+


**Example Get project quotas: JSON response**


.. code::

      {
        "project_quotas": [
          {
              "project_id": "123123",
              "project_quotas": {
                  "secrets": 2000,
                  "orders": 0,
                  "containers": -1,
                  "consumers": 1000,
                  "cas": 0
            }
          },
          {
              "project_id": "789789",
              "project_quotas": {
                  "secrets": 200,
                  "orders": 0,
                  "containers": -1,
                  "consumers": 1000,
                  "cas": 0
            }
          },
        ],
        "total" : 2,
      }
