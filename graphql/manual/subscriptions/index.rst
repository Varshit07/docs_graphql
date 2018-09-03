Subscriptions
=============

A GraphQL subscription is essentially a query where the client receives an event whenever the value of any field changes
upstream. The Hasura GraphQL engine supports subscriptions for all kind of queries. All the concepts of
:doc:`queries <../queries/index>` hold true with subscriptions as well.

You can turn any query into a subscription by simply replacing ``query`` with ``subscription`` as the operation type.

.. admonition:: Caveat

  The `GraphQL spec <http://facebook.github.io/graphql/June2018/#sec-Single-root-field>`_ allows for only one root
  field in a subscription. So though Hasura GraphQL engine supports multiple root fields in subscriptions, most clients
  will not allow it.

**Example:** To keep upto date with the last 2 published articles

.. graphiql::
  :view_only:
  :query:
    subscription {
      article (
        order_by: published_on_desc,
        limit: 2
      ) {
        id
        title
        published_on
        author {
          name
        }
      }
    }
  :response:
    {
      "data": {
        "article": [
          {
            "id": 2,
            "title": "a nibh",
            "published_on": "2018-06-10",
            "author": {
              "name": "Beltran"
            }
          },
          {
            "id": 13,
            "title": "vulputate elementum",
            "published_on": "2018-03-10",
            "author": {
              "name": "April"
            }
          }
        ]
      }
    }

Protocol
--------

Hasura GraphQL engine uses the `GraphQL over Websocket Protocol
<https://github.com/apollographql/subscriptions-transport-ws/blob/master/PROTOCOL.md>`_ by the
`apollographql/subscriptions-transport-ws <https://github.com/apollographql/subscriptions-transport-ws>`_ library
for sending and receiving events.
