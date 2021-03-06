Mutations
=========
GraphQL mutations are used to modify server-side data i.e. write, update or delete data. As with queries, mutation fields are auto-generated on the Postgres schema. Here’s a sample mutation field from our reference Authors/Articles schema:

.. code-block:: none

    insert_article(
      objects: [article_input!] 
      on_conflict: conflict_clause
      ): article_mutation_response

As you can see from the schema, you can:

#. Pass multiple objects to the mutation.
#. Return objects, from the affected rows, in the response.

.. note::
    
    You cannot return a nested object in the response. This is not supported by the GraphQL specification (*we are working on this as a feature*).

Let's use this reference Authors/Articles schema to look at different types of mutations.

.. toctree::
  :maxdepth: 1

  Insert <insert>
  Update <update>
  Delete <delete>
  Upsert <upsert>
  multiple-mutations
  
  











