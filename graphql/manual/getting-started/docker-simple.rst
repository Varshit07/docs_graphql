Run Hasura GraphQL Engine using Docker (Simple)
===============================================

This guide will help you get Hasura Graphql engine and Postgres running as Docker containers using Docker Compose.
This is the easiest way of setting up Hasura on your **local environment**.

**Prerequisites**:

- `Docker <https://docs.docker.com/install/>`_
- `Docker Compose <https://docs.docker.com/compose/install/>`_

Step 1: Install the Hasura CLI
------------------------------

.. rst-class:: api_tabs
.. tabs::

   .. tab:: Mac

      In your terminal enter the following command:

      .. code-block:: bash

        curl -L https://storage.googleapis.com/hasuractl/install-dev.sh | bash

      As this is a preview release of the Hasura CLI, the CLI is named ``hasura-dev`` and not ``hasura``.

   .. tab:: Linux

      Open your linux shell and run the following command:

      .. code-block:: bash

        curl -L https://storage.googleapis.com/hasuractl/install-dev.sh | bash

      As this is a preview release of the Hasura CLI, the CLI is named ``hasura-dev`` and not ``hasura``.

   .. tab:: Windows

       Coming soon ...


Step 2: Initialize a project
----------------------------

.. code-block:: none

  hasura-dev init --directory my-project

Step 3: Run Hasura & Postgres
-----------------------------

.. code-block::  none

   cd my-project/__install
   docker-compose up -d

Check if the containers are running:

.. code-block:: none

  $ docker ps

  CONTAINER ID IMAGE                 ... CREATED STATUS PORTS          ...
  097f58433a2b hasura/graphql-engine ... 1m ago  Up 1m  8080->8080/tcp ...
  b0b1aac0508d postgres              ... 1m ago  Up 1m  5432/tcp       ...

Step 4: Open the hasura console
-------------------------------

In the ``my-project/config.yaml`` file set the endpoint:

.. code-block:: yaml

  endpoint: http://localhost:8080

Now, open the hasura console:

.. code-block:: bash

  # Run this command in the my-project/ directory
  hasura-dev console

Next: Make your first GraphQL query!
------------------------------------

Next, make your :doc:`first graphql query<first-graphql-query>`.