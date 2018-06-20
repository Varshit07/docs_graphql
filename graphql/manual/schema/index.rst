Schema
======

Hasura's GraphQL engine automatically generates your GraphQL schema and resolvers once you create tables or views in Postgres.
You don't need to write a GraphQL schema, you don't need to write resolvers.

Hasura's console gives you UI tools that speed up your data-modelling process or working with your existing database. The console also automatically generates migrations or metadata files that you can edit directly and check into your version control.

Hasura let's you do ANYTHING you usually do with Postgres by giving you GraphQL over native Postgres constructs.

.. toctree::
  :maxdepth: 1

  basics
  relationships
  views
  export-graphql-schema

.. Using your existing database

.. Custom mutations using SQL functions/procedures
.. Using custom postgres extensions and types