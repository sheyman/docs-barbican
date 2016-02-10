.. _Barbican-dg-response-codes:

Response codes
~~~~~~~~~~~~~~~~

Cloud Keep returns an HTTP code that denotes the type of response.

-  Successful response codes are returned only if all configured
   providers were successful in processing the request.

-  Error response codes are accompanied by an ``application/json``
   response body that contains the error messages.

The following table lists possible responses with their associated codes
and descriptions.


**Table: List of response codes**

+--------------------+---------------+-----------------------------------------+
|     Response       | Associated    | Description                             |
|                    | response code |                                         |
+====================+===============+=========================================+
| OK                 | 200           | The request has succeeded. (Some API    |
|                    |               | calls might return 201 instead.)        |
+--------------------+---------------+-----------------------------------------+
| Accepted           | 202           | The request has been accepted for       |
|                    |               | processing.                             |
+--------------------+---------------+-----------------------------------------+
| serviceUnavailable | 503           | The service is currently unavailable.   |
|                    |               | For example, it might be down for       |
|                    |               | scheduled platform maintenance. Try     |
|                    |               | again later.                            |
+--------------------+---------------+-----------------------------------------+

 
**Example: Error message example**

.. code::

    HTTP/1.1 400 Bad Request
    Content-Type: application/json

    {
      "title": "Unsupported limit",
      "description": "The given limit cannot be negative, and cannot be greater than 50.",
      "code": 1092,
      "link": {
        "rel": "help",
        "href": "http://docs.example.com/messages#limit",
        "text": "API documentation for the limit parameter"
      }
    }
