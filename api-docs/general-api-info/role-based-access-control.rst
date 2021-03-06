.. _barbican-dg-rbac:

Role Based Access Control
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Like many other services, the Key Manager service supports the protection of
its APIs by enforcing policy rules defined in a policy file.  The Key Manager
service stores a reference to a policy JSON file in its configuration file,
:file:`/etc/barbican/barbican.conf`.  Typically, this file is named
``policy.json`` and stored in :file:`/etc/barbican/policy.json`.

Each Key Manager API operation has a line in the policy file that dictates which
level of access applies as shown in the following example. 

.. code-block:: ini

    API_NAME: RULE_STATEMENT or MATCH_STATEMENT

The ``RULE_STATEMENT``value can be another ``RULE_STATEMENT`` or a
``MATCH_STATEMENT`` as shown in the following example.

.. code-block:: ini

   RULE_STATEMENT: RULE_STATEMENT or MATCH_STATEMENT

The ``MATCH_STATEMENT`` parameter specifies a set of identifiers that must match 
between the token provided by the caller of the API and the parameters or target 
entities of the API in question.  For example, the following code sample indicates that 
to create a new secret via a POST request, you must have either the admin or creator role 
in your token.

.. code-block:: ini

    "secrets:post": "role:admin or role:creator"


.. warning:: 
    
    The Key Manager service scopes the ownership of a secret at
    the project level.  This means that many calls in the API perform an
    additional check to ensure that the ``project_id`` of the token matches the
    ``project_id`` stored as the secret owner.
    

Default Policy
~~~~~~~~~~~~~~

The policy engine in OpenStack is very flexible and allows for customized
policies that make sense for your particular cloud.  The Key Manager service
comes with a sample ``policy.json`` file which can be used as the starting
point for a customized policy.  The sample policy defines 5 distinct roles:

key-manager:service-admin
    The cloud administrator in charge of the Key Manager service.  This user
    has access to all management APIs like the project-quotas.

admin
    Project administrator.  This user has full access to all resources owned
    by the project for which the admin role is scoped.

creator
    Users with this role are allowed to create new resources but are not
    allowed to delete any existing resources.  They are also allowed full
    access to existing secrets owned by the project in scope.

observer
    Users with this role are allowed to access to existing resources but are
    not allowed to upload new secrets or delete existing secrets.

audit
    Users with this role are only allowed access to the resource metadata.
    So users with this role are unable to decrypt secrets.

Access Control List API
-----------------------

There are some limitations that result from scoping ownership of a secret
at the project level.  For example, there is no easy way for a user to upload
a secret for which only they have access.   There is also no easy way to grant
a user access to only a single secret.
