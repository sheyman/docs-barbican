.. _barbican-dg-concepts:

Concepts
----------

his section describes the key terms and concepts that apply to Rackspace Cloud Keep, and
provides an overview of the Rackspace Cloud Keep architecture.


.. _Barbican-dg-key-terms:

Rackspace Cloud Keep key terms
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _Barbican-dg-secrets:

Secrets
^^^^^^^^^^^^^^^^^^

A secret can be any data that requires security conscious storage. This
may be reflected as a key, credentials, config file, etc.

A secret is a singular item that is stored within Barbican. A secret is
anything you want it to be; however, the formal use case is a key that you wish
to store away from prying eyes.

Some examples of a secret may include:
  * Private Key
  * Certificate
  * Password
  * SSH Keys

The secret schema represents the actual secret or key that is presented
to the application. Currently secrets can be in any format, but
additional functionality may become available in the future for known
types of symmetric or asymmetric keys, like SSL certificates.

The
following shows an example of a secret:

.. code::

    {
        "uuid": "e2b633c7-fda5-4be8-b42c-9a2c9280284d",
        "name": "AES key",
        "expiration": "2014-02-28T19:14:44.180394",
        "secret": "b7990b786ee9659b43e6b1cd6136de07d9c5…",
        "secret_type": "application/aes-256-cbc",
      }

A secret consists of the following elements:

+------------+---------------------------------------------------------------+
| Element    | Description                                                   |
+============+===============================================================+
| uuid       | Unique identifier for the secret. This value is assigned by   |
|            | the API.                                                      |
+------------+---------------------------------------------------------------+
| name       | Human readable name for the secret.                           |
+------------+---------------------------------------------------------------+
| expiration | The expiration date for the secret in ISO-8601 format. Once   |
|            | the secret has expired, it will no longer be returned by the  |
|            | API or agent.                                                 |
+------------+---------------------------------------------------------------+
| secret     | The base64-encoded value of the secret.                       |
+------------+---------------------------------------------------------------+
| secret\_ty | An indication of the type of the file presenting the secret.  |
| pe         |                                                               |
+------------+---------------------------------------------------------------+


You can use one of the following methods to store a secret:

-  Submit a **POST** request against the secrets resource and include
   the secret metadata in the ``payload`` parameter.

-  Submit a **POST** request without a ``payload`` parameter against the
   secrets resource and then include the payload in a subsequent **PUT**
   request. This mode enables you to upload a binary file to the
   Barbican database directly for encrypted storage.

..  note::
        Note
        Submitting a **POST** request creates secret metadata. If the payload is
        provided with the **POST** request, then it is encrypted and stored, and
        then linked with this metadata. If no payload is included with the
        **POST** request, it must be provided with a subsequent **PUT** request.
        The secret resource encrypts and stores client-provided secret
        information and metadata. In contrast, the orders resource generats
        actual secret information on behalf of clients.

.. _Barbican-dg-orders:

Order
^^^^^^^^^^^^^^^^^^

An order is a request to Barbican to create a secret of a particular
type. This may include specifying an encryption algorithm or bit length,
for example.
An order allows for the generation of secret material by
Barbican. The ordering object encapsulates the workflow and history for
the creation of a secret. This interface is implemented as an
asynchronous process since the time to generate a secret can vary
depending on the type of secret.

.. _Barbican-dg-containers:

Container
^^^^^^^^^^^^^^^^^^

A container is a way to logically group secrets that may be of a similar
type; for example, grouping a private key, certificate, and bundle for
an SSL certificate in a single container.
The containers resource is the organizational center piece of Barbican. It
creates a logical object that can be used to hold secret references. This is helpful
when having to deal with tracking and having access to hundreds of secrets.

Barbican supports 3 types of containers:
  * :ref:`Generic <generic_containers>`
  * :ref:`Certificate <certificate_containers>`
  * :ref:`RSA <rsa_containers>`

Each of these types have explicit restrictions as to what type of secrets should be
held within. These will be broken down in their respective sections.

This guide will assume you will be using a local running development environment of Cloud keep_warnings.


.. _generic_containers:

Generic Containers
######################

A generic container is used for any type of container that a user may wish to create.
There are no restrictions on the type or amount of secrets that can be held within a container.

An example of a use case for a generic container would be having multiple passwords stored
in the same container reference:

.. code-block:: json

    {
        "type": "generic",
        "status": "ACTIVE",
        "name": "Test Environment User Passwords",
        "consumers": [],
        "container_ref": "https://{barbican_host}/v1/containers/{uuid}",
        "secret_refs": [
            {
                "name": "test_admin_user",
                "secret_ref": "https://{barbican_host}/v1/secrets/{uuid}"
            },
            {
                "name": "test_audit_user",
                "secret_ref": "https://{barbican_host}/v1/secrets/{uuid}"
            }
        ],
        "created": "2015-03-30T21:10:45.417835",
        "updated": "2015-03-30T21:10:45.417835"
    }


.. _certificate_containers:

Certificate Containers
##########################

A certificate container is used for storing the following secrets that are relevant to
certificates:

  * certificate
  * private_key (optional)
  * private_key_passphrase (optional)
  * intermediates (optional)

.. code-block:: json

    {
        "type": "certificate",
        "status": "ACTIVE",
        "name": "Example.com Certificates",
        "consumers": [],
        "container_ref": "https://{barbican_host}/v1/containers/{uuid}",
        "secret_refs": [
            {
                "name": "certificate",
                "secret_ref": "https://{barbican_host}/v1/secrets/{uuid}"
            },
            {
                "name": "private_key",
                "secret_ref": "https://{barbican_host}/v1/secrets/{uuid}"
            },
            {
                "name": "private_key_passphrase",
                "secret_ref": "https://{barbican_host}/v1/secrets/{uuid}"
            },
            {
                "name": "intermediates",
                "secret_ref": "https://{barbican_host}/v1/secrets/{uuid}"
            }

        ],
        "created": "2015-03-30T21:10:45.417835",
        "updated": "2015-03-30T21:10:45.417835"
    }

The payload for the secret referenced as the "certificate" is expected to be a
PEM formatted x509 certificate.

The payload for the secret referenced as the "intermediates" is expected to be a
PEM formatted PKCS7 certificate chain.


.. _rsa_containers:

RSA Containers
#######################

An RSA container is used for storing RSA public keys, private keys, and private
key pass phrases.

.. code-block:: json

    {
        "type": "rsa",
        "status": "ACTIVE",
        "name": "John Smith RSA",
        "consumers": [],
        "container_ref": "https://{barbican_host}/v1/containers/{uuid}",
        "secret_refs": [
            {
                "name": "private_key",
                "secret_ref": "https://{barbican_host}/v1/secrets/{uuid}"
            },
            {
                "name": "private_key_passphrase",
                "secret_ref": "https://{barbican_host}/v1/secrets/{uuid}"
            },
            {
                "name": "public_key",
                "secret_ref": "https://{barbican_host}/v1/secrets/{uuid}"
            }

        ],
        "created": "2015-03-30T21:10:45.417835",
        "updated": "2015-03-30T21:10:45.417835"
    }


.. _Barbican-dg-certificates:

Certificate
^^^^^^^^^^^^^^^^^^

Certificates are requested using the Orders interface.  Detailed description of this interface
is deferred to the Orders API reference.  This reference identifies the parameters that are specific
to each of the certificate order types i.e. those orders for which the parameter *type*
is "certificate".

.. _Barbican-dg-quotas:

Quotas
^^^^^^^^^^^^^^^^^^

All users authenticated with Cloud Keep are able to read the effective quota values
that apply to their project. Cloud Keep can derive the project that a user belongs
to by reading the project scope from the authentication token.

Service administrators can read, set, and delete quota configurations for each
project known to Barbican.  The service administrator is recognized by his authenticated
role.  The service administrator's role is defined in Barbican's policy.json file.
The default role for a service admin is "key-manager:service-admin".

Quotas can be enforced for the following Cloud Keep resources: secrets, containers,
orders, consumers, and CAs.  The configured quota value can be None (use the default),
-1 (unlimited), 0 (disabled), or a positive integer defining the maximum number
allowed for a project.

.. _default_project_quotas:

Default Quotas
################

When no project quotas have been set for a project, the default
project quotas are enforced for that project.  Default quotas are specified
in the Cloud Keep configuration file (barbican.conf).  The defaults provided
in the standard configuration file are as follows.

.. code-block:: none

    # default number of secrets allowed per project
    quota_secrets = -1

    # default number of orders allowed per project
    quota_orders = -1

    # default number of containers allowed per project
    quota_containers = -1

    # default number of consumers allowed per project
    quota_consumers = -1

    # default number of CAs allowed per project
    quota_cas = -1

The default quotas are returned via a **GET** on the **quotas** resource when no
explicit project quotas have been set for the current project.



.. _Barbican-dg-consumer:


Consumer
^^^^^^^^^^^^^^^^^^

A consumer is a way to to register as an interested party for a container.
All of the registered consumers can be viewed by performing a GET on the {container_ref}/consumers. The idea being that before a container is deleted all consumers
should be notified of the delete.
