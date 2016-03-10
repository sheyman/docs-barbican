
.. _put-configured-project-quotas:

Update configured project quotas
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    PUT /{version}/project-quotas/{project_id}


Create or update the configured project quotas for the project with the specified project ID.



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


This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{project_id}              |String *(Required)*      |This parameter specifies |
|                          |                         |the ID for the           |
|                          |                         |specified project.       |
+--------------------------+-------------------------+-------------------------+

This table shows the parameters for the request:

Request Attributes
******************

+----------------+---------+----------------------------------------------+
| Attribute Name | Type    | Description                                  |
+================+=========+==============================================+
| project-quotas | dict    | A dictionary with project quota information. |
+----------------+---------+----------------------------------------------+
| secrets        | integer | The value to set for this project's secret   |
|                |         | quota.                                       |
+----------------+---------+----------------------------------------------+
| orders         | integer | Reserved for future use.                     |
+----------------+---------+----------------------------------------------+
| containers     | integer | The value to set for this project's          |
|                |         | container quota.                             |
+----------------+---------+----------------------------------------------+
| consumers      | integer | The value to set for this project's          |
|                |         | consumer quota.                              |
+----------------+---------+----------------------------------------------+
| cas            | integer | Reserved for future use.                     |
+----------------+---------+----------------------------------------------+

You only need to specify the values that you want to override.  For example, if
you are only interested in changing the ``secrets`` quota then your project-quotas
dict should only contain an entry for ``secrets``:

.. code::

    {
        "project_quotas": {
                "secrets": 200,
            }
    }

Configured project quota values are specified as follows:

+-------+-----------------------------------------------------------------------------+
| Value | Description                                                                 |
+=======+=============================================================================+
|  -1   | A negative value indicates the resource is unconstrained by a quota.        |
+-------+-----------------------------------------------------------------------------+
|   0   | A zero value indicates that the resource is disabled.                       |
+-------+-----------------------------------------------------------------------------+
| int   | A positive value indicates the maximum number of that resource that can be  |
|       | created for the specified project.                                          |
+-------+-----------------------------------------------------------------------------+
|       | If a value is not given for a resource, this indicates that the default     |
|       | quota should be used for that resource for the specified project.           |
+-------+-----------------------------------------------------------------------------+

**Example update project quotas: JSON request**


.. code::

      curl -s https://{endpoint}/v1/project-quotas/{projectID} \
      -X PUT \
      -d '{
            "project_quotas": {
                "secrets": 50,
                "orders": 10,
                "containers": 20
            }
          }
          ' \
          -H 'X-Auth-Token: {authToken}' \
          -H 'Content-Type: application/json'


where

- {endpoint} is the endpoint for the service
- {authToken} is the authentication token returned by the identity service
- {projectID} is the project ID whose project-level quotas are to be modified



Response
""""""""""""""""

This request does not return a response body.
