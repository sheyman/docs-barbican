
.. _put-secret:

Update Secret
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    PUT /{version}/{tenantId}/secrets/{secret_id}

This method updates a specified secret.

This method updates a secret. To provide secret information after the secret is created, submit a PUT request to the URI that contains the secret ID of the secret you want to update. Note that you can only make PUT request once after a POST call that does not include a payload. Also note that no other attributes of a secret can be modified via PUT.. 				The PUT request should include the payload, as well as the appropriate Content-Type and Content-Encoding definitions.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |Success                  |This status code is      |
|                          |                         |returned when the secret |
|                          |                         |has been successfully    |
|                          |                         |updated.                 |
+--------------------------+-------------------------+-------------------------+
|400                       |Error                    |This error code is       |
|                          |                         |returned when no crypto  |
|                          |                         |plugin supports the      |
|                          |                         |payload_content_type     |
|                          |                         |requested in the Content-|
|                          |                         |Type header.             |
+--------------------------+-------------------------+-------------------------+
|400                       |Error                    |This error code is       |
|                          |                         |returned when no value   |
|                          |                         |was provided for the     |
|                          |                         |"payload" parameter.     |
+--------------------------+-------------------------+-------------------------+
|404                       |Error                    |This error code is       |
|                          |                         |returned when the        |
|                          |                         |supplied UUID doesn't    |
|                          |                         |match the secret in the  |
|                          |                         |datastore for the        |
|                          |                         |specified tenant.        |
+--------------------------+-------------------------+-------------------------+
|409                       |Error                    |This error code is       |
|                          |                         |returned when the secret |
|                          |                         |already has encrypted    |
|                          |                         |data associated with it. |
+--------------------------+-------------------------+-------------------------+
|413                       |Error                    |This error code is       |
|                          |                         |returned when the secret |
|                          |                         |specified in the         |
|                          |                         |"payload" parameter is   |
|                          |                         |too large. The current   |
|                          |                         |size limit is 10,000     |
|                          |                         |bytes.                   |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""


This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{tenantId}                |String *(Required)*      |This parameter specifies |
|                          |                         |the tenant ID of the     |
|                          |                         |client subscribing to    |
|                          |                         |the Barbican service     |
+--------------------------+-------------------------+-------------------------+
|{secret_id}               |String                   |This parameter specifies |
|                          |                         |the unique identifier of |
|                          |                         |a secret that has been   |
|                          |                         |stored.                  |
+--------------------------+-------------------------+-------------------------+





This operation does not accept a request body.


**Example Update Secret: JSON request**


.. code::

   curl -i -X PUT -H 'Content-Type: application/octet-stream' \
        -T ./secret_key_file http://endpointURL/v1/12345/secrets/a83018d1-e657-4957-9ddd-42a479753e6b



Response
""""""""""""""""


**Example Update Secret: JSON response**


.. code::

   HTTP/1.1 200 OK
   Content-Length: 0
   x-openstack-request-id: req-ab107dce-adfd-4b8d-b9eb-7095f8cf9b15
