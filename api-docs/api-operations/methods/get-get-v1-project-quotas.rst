
.. _get-project-quotas:

Get project quotas
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /{version}/quotas

Get the effective quotas for the project of the requester. The project id
of the requester is derived from the authentication token provided in the
X-Auth-Token header.


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


There are no URL parameters for this request.


This operation does not accept a request body.


**Example Get project quotas: JSON request**


.. code::

   curl -H 'Accept: application/json' -H 'X-Auth-Token:{authToken}'\
   https://{endpoint}/v1/quotas

where

- {endpoint} is the endpoint for the service
- {authToken} is the authentication token returned by the identity service


Response
""""""""""""""""

This table shows the response attributes for this request.

+------------+---------+--------------------------------------------------------------+
| Name       | Type    | Description                                                  |
+============+=========+==============================================================+
| quotas     | dict    | Contains a dictionary with quota information                 |
+------------+---------+--------------------------------------------------------------+
| secrets    | integer | Contains the effective quota value of the current project    |
|            |         | for the secret resource.                                     |
+------------+---------+--------------------------------------------------------------+
| orders     | integer | Reserved for future use.                                     |
+------------+---------+--------------------------------------------------------------+
| containers | integer | Contains the effective quota value of the current project    |
|            |         | for the containers resource.                                 |
+------------+---------+--------------------------------------------------------------+
| consumers  | integer | Contains the effective quota value of the current project    |
|            |         | for the consumers resource.                                  |
+------------+---------+--------------------------------------------------------------+
| cas        | integer | Reserved for future use.                                     |
+------------+---------+--------------------------------------------------------------+

Effective quota values are interpreted as follows:

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

**Example Get project quotas: JSON response**


.. code::

    {
      "quotas": {
        "secrets": 1000,
        "cas": 0,
        "orders": 0,
        "containers": 1000,
        "consumers": 1000
      }
    }
