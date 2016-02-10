
.. _get-project-quotas:

Get project quotas
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /{version}/{tenantId}/quotas

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


This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{tenantId}                |String *(Required)*      |This parameter specifies |
|                          |                         |the tenant ID of the     |
|                          |                         |client subscribing to    |
|                          |                         |the Cloud Keep service.  |
+--------------------------+-------------------------+-------------------------+


This operation does not accept a request body.


**Example Get project quotas: JSON request**


.. code::

   curl -H 'Accept: application/json' -H 'X-Auth-Token:<token>'\
   https://endpointURL/v1/quotas


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
| orders     | integer | Contains the effective quota value of the current project    |
|            |         | for the orders resource.                                     |
+------------+---------+--------------------------------------------------------------+
| containers | integer | Contains the effective quota value of the current project    |
|            |         | for the containers resource.                                 |
+------------+---------+--------------------------------------------------------------+
| consumers  | integer | Contains the effective quota value of the current project    |
|            |         | for the consumers resource.                                  |
+------------+---------+--------------------------------------------------------------+
| cas        | integer | Contains the effective quota value of the current project    |
|            |         | for the CAs resource.                                        |
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

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
          "quotas": {
            "secrets": 10,
            "orders": 20,
            "containers": 10,
            "consumers": -1,
            "cas": 5
         }
       }
