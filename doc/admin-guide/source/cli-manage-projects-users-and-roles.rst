=================================
Manage projects, users, and roles
=================================

As an administrator, you manage projects, users, and
roles. Projects are organizational units in the cloud to which
you can assign users. Projects are also known as *projects* or
*accounts*. Users can be members of one or more projects. Roles
define which actions users can perform. You assign roles to
user-project pairs.

You can define actions for OpenStack service roles in the
``/etc/PROJECT/policy.json`` files. For example, define actions for
Compute service roles in the ``/etc/nova/policy.json`` file.

You can manage projects, users, and roles independently from each other.

During cloud set up, the operator defines at least one project, user,
and role.

You can add, update, and delete projects and users, assign users to
one or more projects, and change or remove the assignment. To enable or
temporarily disable a project or user, update that project or user.
You can also change quotas at the project level.

Before you can delete a user account, you must remove the user account
from its primary project.

Before you can run client commands, you must download and
source an OpenStack RC file. See `Download and source the OpenStack RC file
<http://docs.openstack.org/user-guide/common/cli-set-environment-variables-using-openstack-rc.html#download-and-source-the-openstack-rc-file>`_.

Projects
~~~~~~~~

A project is a group of zero or more users. In Compute, a project owns
virtual machines. In Object Storage, a project owns containers. Users
can be associated with more than one project. Each project and user
pairing can have a role associated with it.

List projects
-------------

List all projects with their ID, name, and whether they are
enabled or disabled:

.. code-block:: console

   $ openstack project list
   +----------------------------------+--------------------+
   | ID                               | Name               |
   +----------------------------------+--------------------+
   | f7ac731cc11f40efbc03a9f9e1d1d21f | admin              |
   | c150ab41f0d9443f8874e32e725a4cc8 | alt_demo           |
   | a9debfe41a6d4d09a677da737b907d5e | demo               |
   | 9208739195a34c628c58c95d157917d7 | invisible_to_admin |
   | 3943a53dc92a49b2827fae94363851e1 | service            |
   | 80cab5e1f02045abad92a2864cfd76cb | test_project       |
   +----------------------------------+--------------------+

Create a project
----------------

Create a project named ``new-project``:

.. code-block:: console

   $ openstack project create --description 'my new project' new-project \
     --domain default
   +-------------+----------------------------------+
   | Field       | Value                            |
   +-------------+----------------------------------+
   | description | my new project                   |
   | domain_id   | e601210181f54843b51b3edff41d4980 |
   | enabled     | True                             |
   | id          | 1a4a0618b306462c9830f876b0bd6af2 |
   | is_domain   | False                            |
   | name        | new-project                      |
   | parent_id   | e601210181f54843b51b3edff41d4980 |
   +-------------+----------------------------------+

Update a project
----------------

Specify the project ID to update a project. You can update the name,
description, and enabled status of a project.

-  To temporarily disable a project:

   .. code-block:: console

      $ openstack project set PROJECT_ID --disable

-  To enable a disabled project:

   .. code-block:: console

      $ openstack project set PROJECT_ID --enable

-  To update the name of a project:

   .. code-block:: console

      $ openstack project set PROJECT_ID --name project-new

-  To verify your changes, show information for the updated project:

   .. code-block:: console

      $ openstack project show PROJECT_ID
      +-------------+----------------------------------+
      | Field       | Value                            |
      +-------------+----------------------------------+
      | description | my new project                   |
      | enabled     | True                             |
      | id          | 0b0b995694234521bf93c792ed44247f |
      | name        | new-project                      |
      | properties  |                                  |
      +-------------+----------------------------------+

Delete a project
----------------

Specify the project ID to delete a project:

.. code-block:: console

   $ openstack project delete PROJECT_ID

Users
~~~~~

List users
----------

List all users:

.. code-block:: console

   $ openstack user list
   +----------------------------------+----------+
   | ID                               | Name     |
   +----------------------------------+----------+
   | 352b37f5c89144d4ad0534139266d51f | admin    |
   | 86c0de739bcb4802b8dc786921355813 | demo     |
   | 32ec34aae8ea432e8af560a1cec0e881 | glance   |
   | 7047fcb7908e420cb36e13bbd72c972c | nova     |
   +----------------------------------+----------+

Create a user
-------------

To create a user, you must specify a name. Optionally, you can
specify a project ID, password, and email address. It is recommended
that you include the project ID and password because the user cannot
log in to the dashboard without this information.

Create the ``new-user`` user:

.. code-block:: console

   $ openstack user create --project new-project --password PASSWORD new-user
   +------------+----------------------------------+
   | Field      | Value                            |
   +------------+----------------------------------+
   | email      | None                             |
   | enabled    | True                             |
   | id         | 6322872d9c7e445dbbb49c1f9ca28adc |
   | name       | new-user                         |
   | project_id | 0b0b995694234521bf93c792ed44247f |
   | username   | new-user                         |
   +------------+----------------------------------+

Update a user
-------------

You can update the name, email address, and enabled status for a user.

-  To temporarily disable a user account:

   .. code-block:: console

      $ openstack user set USER_NAME --disable

   If you disable a user account, the user cannot log in to the
   dashboard. However, data for the user account is maintained, so you
   can enable the user at any time.

-  To enable a disabled user account:

   .. code-block:: console

      $ openstack user set USER_NAME --enable

-  To change the name and description for a user account:

   .. code-block:: console

      $ openstack user set USER_NAME --name user-new --email new-user@example.com
      User has been updated.

Delete a user
-------------

Delete a specified user account:

.. code-block:: console

   $ openstack user delete USER_NAME

Roles and role assignments
~~~~~~~~~~~~~~~~~~~~~~~~~~

List available roles
--------------------

List the available roles:

.. code-block:: console

   $ openstack role list
   +----------------------------------+---------------+
   | ID                               | Name          |
   +----------------------------------+---------------+
   | 71ccc37d41c8491c975ae72676db687f | Member        |
   | 149f50a1fe684bfa88dae76a48d26ef7 | ResellerAdmin |
   | 9fe2ff9ee4384b1894a90878d3e92bab | _member_      |
   | 6ecf391421604da985db2f141e46a7c8 | admin         |
   | deb4fffd123c4d02a907c2c74559dccf | anotherrole   |
   +----------------------------------+---------------+

Create a role
-------------

Users can be members of multiple projects. To assign users to multiple
projects, define a role and assign that role to a user-project pair.

Create the ``new-role`` role:

.. code-block:: console

   $ openstack role create new-role
   +-----------+----------------------------------+
   | Field     | Value                            |
   +-----------+----------------------------------+
   | domain_id | None                             |
   | id        | a34425c884c74c8881496dc2c2e84ffc |
   | name      | new-role                         |
   +-----------+----------------------------------+

Assign a role
-------------

To assign a user to a project, you must assign the role to a
user-project pair. To do this, you need the user, role, and project
IDs.

#. List users and note the user ID you want to assign to the role:

   .. code-block:: console

      $ openstack user list
      +----------------------------------+----------+
      | ID                               | Name     |
      +----------------------------------+----------+
      | 6ab5800949644c3e8fb86aaeab8275c8 | admin    |
      | dfc484b9094f4390b9c51aba49a6df34 | demo     |
      | 55389ff02f5e40cf85a053cc1cacb20c | alt_demo |
      | bc52bcfd882f4d388485451c4a29f8e0 | nova     |
      | 255388ffa6e54ec991f584cb03085e77 | glance   |
      | 48b6e6dec364428da89ba67b654fac03 | cinder   |
      | c094dd5a8e1d4010832c249d39541316 | neutron  |
      | 6322872d9c7e445dbbb49c1f9ca28adc | new-user |
      +----------------------------------+----------+

#. List role IDs and note the role ID you want to assign:

   .. code-block:: console

      $ openstack role list
      +----------------------------------+---------------+
      | ID                               | Name          |
      +----------------------------------+---------------+
      | 71ccc37d41c8491c975ae72676db687f | Member        |
      | 149f50a1fe684bfa88dae76a48d26ef7 | ResellerAdmin |
      | 9fe2ff9ee4384b1894a90878d3e92bab | _member_      |
      | 6ecf391421604da985db2f141e46a7c8 | admin         |
      | deb4fffd123c4d02a907c2c74559dccf | anotherrole   |
      | bef1f95537914b1295da6aa038ef4de6 | new-role      |
      +----------------------------------+---------------+

#. List projects and note the project ID you want to assign to the role:

   .. code-block:: console

      $ openstack project list
      +----------------------------------+--------------------+
      | ID                               | Name               |
      +----------------------------------+--------------------+
      | 0b0b995694234521bf93c792ed44247f | new-project        |
      | 29c09e68e6f741afa952a837e29c700b | admin              |
      | 3a7ab11d3be74d3c9df3ede538840966 | invisible_to_admin |
      | 71a2c23bab884c609774c2db6fcee3d0 | service            |
      | 87e48a8394e34d13afc2646bc85a0d8c | alt_demo           |
      | fef7ae86615f4bf5a37c1196d09bcb95 | demo               |
      +----------------------------------+--------------------+

#. Assign a role to a user-project pair:

   .. code-block:: console

      $ openstack role add --user USER_NAME --project TENANT_ID ROLE_NAME

   For example, assign the ``new-role`` role to the ``demo`` and
   ``test-project`` pair:

   .. code-block:: console

      $ openstack role add --user demo --project test-project new-role

#. Verify the role assignment:

   .. code-block:: console

      $ openstack role list --user USER_NAME --project TENANT_ID
      Listing assignments using role list is deprecated as of the Newton release. Use role assignment list --user <user-name> --project <project-name> --names instead.
      +----------------------------------+-------------+---------+------+
      | ID                               | Name        | Project | User |
      +----------------------------------+-------------+---------+------+
      | a34425c884c74c8881496dc2c2e84ffc | new-role    | demo    | demo |
      | 04a7e3192c0745a2b1e3d2baf5a3ee0f | Member      | demo    | demo |
      | 62bcf3e27eef4f648eb72d1f9920f6e5 | anotherrole | demo    | demo |
      +----------------------------------+-------------+---------+------+

View role details
-----------------

View details for a specified role:

.. code-block:: console

   $ openstack role show ROLE_NAME
   +-----------+----------------------------------+
   | Field     | Value                            |
   +-----------+----------------------------------+
   | domain_id | None                             |
   | id        | a34425c884c74c8881496dc2c2e84ffc |
   | name      | new-role                         |
   +-----------+----------------------------------+

Remove a role
-------------

Remove a role from a user-project pair:

#. Run the :command:`openstack role remove` command:

   .. code-block:: console

      $ openstack role remove --user USER_NAME --project TENANT_ID ROLE_NAME

#. Verify the role removal:

   .. code-block:: console

      $ openstack role list --user USER_NAME --project TENANT_ID

   If the role was removed, the command output omits the removed role.
