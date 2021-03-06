
.. _get-project-quota-records:

Get Project quota records
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

  GET /v1/project-quotas

Gets a list of configured project quota records.  Paging is supported using the
optional parameters offset and limit.


The following table shows the possible response codes for this operation:


+------+-----------------------------------------------------------------------------+
| Code | Description                                                                 |
+======+=============================================================================+
| 200  | Successful Request                                                          |
+------+-----------------------------------------------------------------------------+
| 401  | Invalid X-Auth-Token or the token doesn't have permissions to this resource |
+------+-----------------------------------------------------------------------------+


Request
""""""""""""""""

The following table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{tenantId}                |String *(Required)*      |This parameter specifies |
|                          |                         |the tenant ID of the     |
|                          |                         |client subscribing to    |
|                          |                         |the Cloud Keep service.  |
+--------------------------+-------------------------+-------------------------+


The following table shows the body parameters for the request:


+--------+---------+----------------------------------------------------------------+
| Name   | Type    | Description                                                    |
+========+=========+================================================================+
| offset | integer | The starting index within the total list of the project        |
|        |         | quotas that you would like to receive.                         |
+--------+---------+----------------------------------------------------------------+
| limit  | integer | The maximum number of records to return.                       |
+--------+---------+----------------------------------------------------------------+


**Example: Get project quotas cURL request**


.. code::

   curl -H 'Accept: application/json' \
        -H 'X-Auth-Token:<token>'\
        $ENDPOINT/{version}/project-quotas


Response
""""""""""""""""

The following table shows the response parameters for the request.


+------------------+---------+-----------------------------------------------------------+
| Name             | Type    | Description                                               |
+==================+=========+===========================================================+
|**project-quotas**| list    | Returns a list of project quota configurations            |
+------------------+---------+-----------------------------------------------------------+
|**project-quotas**| dict    | Contains a dictionary with project quota information.     |
+------------------+---------+-----------------------------------------------------------+
|project-quotas.\ | integer | The ID of the project associated with the project quota    |
|**project_id**   |         |                                                            |
+-----------------+---------+------------------------------------------------------------+
|project-quotas.\ | integer | Contains the effective quota value of the current project  |
|*secrets*        |         | for the secret resource.                                   |
+-----------------+---------+------------------------------------------------------------+
|project-quotas.\ | integer | Contains the effective quota value of the current project  |
|**orders**       |         | for the orders resource.                                   |
+-----------------+---------+------------------------------------------------------------+
|project-quotas.\ | integer | Contains the effective quota value of the current project  |
|**containers**   |         | for the containers resource.                               |
+-----------------+---------+------------------------------------------------------------+
|project-quotas.\ | integer | Contains the effective quota value of the current project  |
|**consumers**    |         | for the consumers resource.                                |
+-----------------+---------+------------------------------------------------------------+
|project-quotas.\ | integer | Contains the effective quota value of the current project  |
|**cas**          |         | for the CAs resource.                                      |
+-----------------+---------+------------------------------------------------------------+
|**total**        | integer | The total number of configured project quotas records.     |
+-----------------+---------+------------------------------------------------------------+
|**next**         | string  | A HATEOAS url to retrieve the next set of quotas based on  |
|                 |         | the offset and limit parameters. This attribute is only    |
|                 |         | available when the total number of secrets is greater than |
|                 |         | offset and limit parameter combined.                       |
+-----------------+---------+------------------------------------------------------------+
| previous        | string  | A HATEOAS url to retrieve the previous set of quotas based |
|                 |         | on the offset and limit parameters. This attribute is only |
|                 |         | available when the request offset is greater than 0.       |
+-----------------+---------+------------------------------------------------------------+


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


**Example: Get project quotas JSON response**


.. code::

      200 OK

      Content-Type: application/json

      {
        "project_quotas": [
          {
              "project_id": "1234",
              "project_quotas": {
                  "secrets": 2000,
                  "orders": 0,
                  "containers": -1,
                  "consumers": null,
                  "cas": null
            }
          },
          {
              "project_id": "5678",
              "project_quotas": {
                  "secrets": 200,
                  "orders": 100,
                  "containers": -1,
                  "consumers": null,
                  "cas": null
            }
          },
        ],
        "total" : 30,
      }
