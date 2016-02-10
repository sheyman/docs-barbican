
.. _get-containers-consumers:

Get a container's consumers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /{container_ref}/consumers


Lists a container's consumers.

The list of consumers can be filtered by the parameters passed in via the URL.

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


The following table shows the URI parameters for the request:

+----------+---------+----------------------------------------------------------------+
| Name     | Type    | Description                                                    |
+==========+=========+================================================================+
| offset   | integer | The starting index within the total list of the consumers that |
|          |         | you would like to retrieve.                                    |
+----------+---------+----------------------------------------------------------------+
| limit    | integer | The maximum number of records to return (up to 100). The       |
|          |         | default limit is 10.                                           |
+----------+---------+----------------------------------------------------------------+


**Example Get container's consumers: JSON request**


.. code::

   curl -H 'Accept: application/json' -H 'X-Project-Id:12345'\
   https://endpointURL/v1/{container_ref}/consumers



**Example Get container's consumers with offset and limit parameters: JSON request**


   .. code::

      curl -H 'Accept: application/json' -H 'X-Project-Id:12345'\
      https://endpointURL/v1/{container_ref}/consumers?limit=1&offset=1


Response
""""""""""""""""

The following table shows the response parameters for this request.

+----------+---------+---------------------------------------------------------------+
| Name     | Type    | Description                                                   |
+==========+=========+===============================================================+
|consumers | list    | Contains a list of dictionaries filled with consumer metadata.|
+----------+---------+---------------------------------------------------------------+
| total    | integer | The total number of consumers available to the user.          |
+----------+---------+---------------------------------------------------------------+
| next     | string  | A HATEOAS url to retrieve the next set of consumers based on  |
|          |         | the offset and limit parameters. This attribute is only       |
|          |         | available when the total number of consumers is greater than  |
|          |         | offset and limit parameter combined.                          |
+----------+---------+---------------------------------------------------------------+
| previous | string  | A HATEOAS url to retrieve the previous set of consumers based |
|          |         | on the offset and limit parameters. This attribute is only    |
|          |         | available when the request offset is greater than 0.          |
+----------+---------+---------------------------------------------------------------+

**Example Get container's consumers: JSON response**


.. code::

      {
        "total": 3,
        "consumers": [
          {
              "status": "ACTIVE",
              "URL": "consumerurl",
              "updated": "2015-10-15T21:06:33.123878",
              "name": "consumername",
              "created": "2015-10-15T21:06:33.123872"
          },
          {
              "status": "ACTIVE",
              "URL": "consumerURL2",
              "updated": "2015-10-15T21:17:08.092416",
              "name": "consumername2",
              "created": "2015-10-15T21:17:08.092408"
          },
          {
              "status": "ACTIVE",
              "URL": "consumerURL3",
              "updated": "2015-10-15T21:21:29.970370",
              "name": "consumername3",
              "created": "2015-10-15T21:21:29.970365"
          }
        ]
      }

**Example Get container's consumers with offset and limit parameters: JSON response**

.. code::

     {
         "total": 3,
         "next": "http://localhost:9311/v1/consumers?limit=1&offset=2",
         "consumers": [
            {
                "status": "ACTIVE",
                "URL": "consumerURL2",
                "updated": "2015-10-15T21:17:08.092416",
                "name": "consumername2",
                "created": "2015-10-15T21:17:08.092408"
            }
        ],
        "previous": "http://localhost:9311/v1/consumers?limit=1&offset=0"
     }
