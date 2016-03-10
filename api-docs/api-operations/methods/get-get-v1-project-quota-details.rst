
.. _get-project-quota-details:

Get Project quota details
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /{version}/project-quotas/{project_id}

Retrieves the specified project's configured project quota information.  This is different
from the GET /{version}/quotas API call which returns the resolved quotas.  This call only
returns the values set for quotas at the project level.  Quotas are resolved by taking the
system level of quotas and overriding any project-level quotas.

This table shows the possible response codes for this operation:

+------+-----------------------------------------------------------------------------+
| Code | Description                                                                 |
+======+=============================================================================+
| 200  | Successful request                                                          |
+------+-----------------------------------------------------------------------------+
| 401  | Invalid X-Auth-Token or the token doesn't have permissions to this resource |
+------+-----------------------------------------------------------------------------+
| 404  | Not Found.  The requested project does not have any configured quotas.      |
+------+-----------------------------------------------------------------------------+


Request
""""""""""""""""

This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{project_id}              |String                   |This parameter specifies |
|                          |                         |the unique identifier of |
|                          |                         |a project.               |
+--------------------------+-------------------------+-------------------------+


This operation does not accept a request body.


**Example Get project quota details: JSON request**


.. code::

   curl -H 'Accept: application/json' -H 'X-Auth-Token:{authToken}'\
   https://{endpoint}/v1/project-quotas/{projectID}

where:

- {endpoint} is the endpoint for the service
- {authToken} is the authentication token returned by the identity service
- {projectID} is the id of the project


Response
""""""""""""""""

The following table shows the response attributes for this request.

+----------------+---------+--------------------------------------------------------------+
| Name           | Type    | Description                                                  |
+================+=========+==============================================================+
| project-quotas | dict    | Contains a dictionary with project quota information.        |
+----------------+---------+--------------------------------------------------------------+
| secrets        | integer | Contains the configured quota value of the requested project |
|                |         | for the secrets resource.                                    |
+----------------+---------+--------------------------------------------------------------+
| orders         | integer | Reserved for future use.                                     |
+----------------+---------+--------------------------------------------------------------+
| containers     | integer | Contains the configured quota value of the requested project |
|                |         | for the containers resource.                                 |
+----------------+---------+--------------------------------------------------------------+
| consumers      | integer | Contains the configured quota value of the requested project |
|                |         | for the consumers resource.                                  |
+----------------+---------+--------------------------------------------------------------+
| cas            | integer |  Reserved for future use.                                    |
+----------------+---------+--------------------------------------------------------------+


**Example Get Project quota details: JSON response**


.. code::

        {
            "project_quotas": {
                "secrets": 10,
                "orders": 0,
                "containers": -1,
                "consumers": 10,
                "cas": 0
                }
        }
