Using your existing database
============================

Let's say you have a Postgres database with data in it, and you'd like to get instant GraphQL on it.

This section assumes that you already have Hasura and Postgres setup. If you want to run Hasura with an existing
database head to :doc:`Setup with Docker (advanced) <docker-advanced>` or
:doc:`Setup on Heroku (advanced) <heroku-advanced>`.

As a tutorial, this section will use a sample dataset that we'll import to see how Hasura works with existing databases.

Step 1 (optional): Import a sample dataset
------------------------------------------

You can skip this step if your postgres database already has data.

Let's use the `Chinook database <https://raw.githubusercontent.com/xivSolutions/ChinookDb_Pg_Modified/pg_names/chinook_pg_serial_pk_proper_naming.sql>`_ as an example.

.. code-block:: bash

  $ wget https://raw.githubusercontent.com/xivSolutions/ChinookDb_Pg_Modified/pg_names/chinook_pg_serial_pk_proper_naming.sql
  $ psql --echo-errors -h 127.0.0.1 -p 5432 -U postgres -d postgres < chinook_pg_serial_pk_proper_naming.sql
  ..
  ..
  ..
  CREATE INDEX
  CREATE TRIGGER
  CREATE TRIGGER
  ALTER TABLE
  CREATE INDEX
  CREATE TRIGGER
  ALTER TABLE

Step 2: Open the hasura console
-------------------------------

Now, open the hasura console:

.. code-block:: bash

  # Run this command in the my-project/ directory
  $ hasura console

Navigate to `http://localhost:9695/data/schema <http://localhost:9695/data/schema>`_

You should see the list of tables which are yet to be tracked in your public schema. It should look like the screenshot below

.. image:: ../../../img/graphql/manual/getting-started/UntrackedTables.jpg
  :alt: List of untracked tables

Click on the ``Add all`` button as shown in the image below to track all the tables.

.. image:: ../../../img/graphql/manual/getting-started/TrackTable.jpg
  :alt: Track the list of untracked table

Once all the tables are tracked, you'll see that tables come up in the sidebar:

.. image:: ../../../img/graphql/manual/getting-started/TableTracked.jpg
  :alt: Tables successfully tracked


Now we have successfully tracked the tables, let's open API Explorer and make a GraphQL query:


.. image:: ../../../img/graphql/manual/getting-started/GraphQLAPI.jpg
  :alt: Make a simple fetch call to query actors

.. code-block:: none

  # Query                  |            # Response
  query {                  |            {
    actors {               |              "data": {
      id                   |                "actors": [
      first_name           |                  {
      last_name            |                    "id": 1,
    }                      |                    "first_name": "Penelope",
  }                        |                    "last_name": "Guiness"
                           |                  },
                           |                  // ...
                           |                ]
                           |              }
                           |            }
