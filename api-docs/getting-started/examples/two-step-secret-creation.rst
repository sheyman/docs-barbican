.. _gsg-two-step-secret-creation:


Create a secret using two-step storage 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can use a two-step secret storage process when secret data cannot be
easily provided inside the JSON data in a one-step secret storage.

#. To follow the two-step process, first create the secret metadata in
   Barbican by sending a **POST** request as shown in the following
   example:

   .. code::

        curl -i -H 'Content-Type: application/json' -d '{"name": "Binary Key File"}' http://endpointURL/v1/12345/secrets

   If the call is successfull, you receive a ``200 OK`` response as
   shown in the following example:

   .. code::

        HTTP/1.1 201 Created
        Content-Length: 93
         Content-Type: application/json; charset=utf-8
       Location: http://endpointURL/12345/secrets/a83018d1-e657-4957-9ddd-42a479753e6b
        x-openstack-request-id: req-ea090bd4-5bfc-47ae-a388-746485d947f1

        {
          "secret_ref": "http://endpointURL/v1/12345/secrets/a83018d1-e657-4957-9ddd-42a479753e6b”
        }

   The secret metadata is now stored in Barbican. You still need to
   provide the actual secret, therefore be sure to save the
   ``secret_ref`` information as you will need it for uploading the
   secret data.

#. Next, create a file with random data to be used as a secret key file.
   The following command creates a 5KB file that contains random data in
   the current directory:

   .. code::

        dd if=/dev/random of=secret_key_file count=5 bs=1024

#. Next, submit a **PUT** request that includes the secret key file you
   just created as sghown in the following example:

   .. code::

        curl -i -X PUT -H 'Content-Type: application/octet-stream’ \
             -T ./secret_key_file http://endpointURL/v1/12345/secrets/a83018d1-e657-4957-9ddd-42a479753e6b

#. Barbican encrypts and stores the secret key file, associates it with
   the previously created metadata, and responds with an empty
   ``200 OK`` message as shown in the following example:

   .. code::

        HTTP/1.1 200 OK Content-Length: 0 x-openstack-request-id: req-ab107dce-adfd-4b8d-b9eb-7095f8cf9b15

Now you can use a **GET** request to retrieve the secret, as explained
in `Retrieving a secret <sg-retrieve-a-secret>`__.
