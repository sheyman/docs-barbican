
.. _put-secret:

Update Secret
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    PUT /{version}/secrets/{secret_id}

This method stores a payload for the specified secret.

This method sets the payload for an existing secret when that secret was created without a payload.
To provide secret information after the secret is created, submit a PUT request to the URI that contains the secret ID of the secret you want to update. Note that you can only make PUT request once after a POST call that does not include a payload. Also note that no other attributes of a secret can be modified via PUT.  The PUT request should include the payload, as well as the appropriate Content-Type and Content-Encoding definitions.


This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|204                       |No Content               |This status code is      |
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
|                          |                         |match a secret in the    |
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
|{secret_id}               |String                   |This parameter specifies |
|                          |                         |the unique identifier of |
|                          |                         |a secret that has been   |
|                          |                         |stored.                  |
+--------------------------+-------------------------+-------------------------+





This operation does not accept a request body.


**Example Update Secret: JSON request**


.. code::

   curl -X PUT -H 'Content-Type: application/octet-stream' -H 'X-Auth-Token: {authToken}' \
        -T {secretDataFile} https://{endpoint}/v1/secrets/a83018d1-e657-4957-9ddd-42a479753e6b

where:

- {endpoint} is the endpoint for the service
- {authToken} is the authentication token returned by the identity service
- {secretDataFile} is a file containing the binary data to be stored as the secret payload.

..  note::
    The -T option to curl is used to send the contents of the specified file as the body of the
    request.  For more information see https://curl.haxx.se/docs/manual.html.


Response
""""""""""""""""


**Example Update Secret: JSON response**


The successful response will be an HTTP 204 return code, with no content.
