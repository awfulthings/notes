Graphql basics

1. https://www.prisma.io/blog/graphql-server-basics-the-schema-ac5e2950214e/
2. https://www.prisma.io/blog/graphql-server-basics-the-network-layer-51d97d21861/
3. https://www.prisma.io/blog/graphql-server-basics-demystifying-the-info-argument-in-graphql-resolvers-6f26249f613a/


GraphQL Server Basics: GraphQL Schemas, TypeDefs & Resolvers Explained

Schema

Type defines the structure of a model in your application.

Root types define entry points for graphic api:
- Query
- Mutation
- Subscription

Dataloader

Optimalizace dotazů na databázi: https://www.youtube.com/watch?v=OQTnXNCDywA

Resolvery

* root (also sometimes called parent): Remember how we said all a GraphQL server needs to do to resolve a query is calling the resolvers of the query’s fields? Well, it’s doing so breadth-first (level-by-level) and the root argument in each resolver call is simply the result of the previous call (initial value is null if not otherwise specified).
* args: This argument carries the parameters for the query, in this case the id of the User to be fetched.
* context: An object that gets passed through the resolver chain that each resolver can write to and read from (basically a means for resolvers to communicate and share information).
* info: An AST representation of the query or mutation. You can read more about the details in part III of this series: Demystifying the info Argument in GraphQL Resolvers.

Nejdřív se volá resolver na celý objekt (root field). Potom resolvery pro jednotlivé parametry objektu.



GraphQL Server Basics: The Network Layer

V JS se používá graphql server jako middleware:
- express-graphql (je od facebooku)
- apollo-server (podporuje víc server libraries)
- graphql-yoga (umí file uploads a zjednodušuje implementaci subscriptions)


GraphQL Server Basics: Demystifying the `info` Argument in GraphQL Resolvers

Info object - obsahuje informace o parent typu, return typu a strom celého query.










