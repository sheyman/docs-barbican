
.. _delete-project-quota-configuration:

Delete the project quotas configuration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    DELETE /v1/project-quotas/{project_id}

Delete the project quotas configuration for the project with the specified project_id. When
the project quota configuration is deleted, then the default quotas will be used for
the specified project.

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

This operation does not accept a request body.


**Example Delete project quota: JSON request**


.. code::

      curl -X DELETE -H 'X-Auth-Token: {authToken}' \
        https://{endpoint}/v1/project-quotas/{projectID}

where:
 
 - {endpoint} is the endpoint for the service
 - {authToken} is the authentication token returned by the identity service
 - {projectID} is the ID for the project whose project-level quotas are to be deleted.


Response
""""""""""""""""

This operation does not return a response body.
