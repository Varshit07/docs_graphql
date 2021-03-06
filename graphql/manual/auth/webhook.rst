Authorization Webhook
=====================

You can configure a webhook (see :doc:`GraphQL Server Options <../deployment/options>`) to authenticate all incoming requests to Hasura GraphQL server.

.. image:: ../../../img/graphql/manual/auth/webhook-auth.png

.. note::
   Configuring webhook requires Hasura to run with an access key (``--access-key``).
..   :doc:`Read more<config>`.


- The configured webook is  **called** when ``X-Hasura-Access-Key`` header is not found in the request.
- The configured webhook is **ignored** when ``X-Hasura-Access-Key`` header is found in the request.


Spec for the webhook
--------------------

Request
^^^^^^^
Hasura will send ``GET`` request to you webhook with **all headers it received from client**

.. code-block:: http

   GET https://<your-custom-webhook>/ HTTP/1.1
   <Header-Key>: <Header-Value>

Response
^^^^^^^^

Success
+++++++
To allow the GraphQL request to go through, your webhook must return a ``200`` status code.
You should send the ``X-Hasura-*`` "session variables" your permission rules in Hasura.

.. code-block:: http

   HTTP/1.1 200 OK
   Content-Type: application/json

   {
       "X-Hasura-User-Id": "25",
       "X-Hasura-Role": "user",
       "X-Hasura-Is-Owner": "true",
       "X-Hasura-Custom": "custom value"
   }

.. note::
   All values should be ``String``, they will be converted to the right type automatically.

Failure
+++++++
If you want to deny the GraphQL request return a ``401 Unauthorized`` exception.

.. code-block:: http

   HTTP/1.1 401 Unauthorized

.. note::
   Anything other than ``200`` or ``401`` response from webhook then server raises ``500 Internal Server Error`` exception
