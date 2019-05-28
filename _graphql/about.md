---
title: About GraphQL
position: 1.0
description: GraphQL is a powerful API query language
---

GraphQL is a data query language which provides an alternative to REST and ad-hoc web service architectures. It allows clients to define the structure of the data required, and exactly the same structure of the data is returned from the server. It is a strongly typed runtime which allows clients to dictate what data is needed, therefore preventing excessively large amounts of data being returned.

Memair's implementation of GraphQL allows for large (10,000 records) import and export of data per query or mutation. Create mutations are processed in the background and you can monitor the jobs progress using the [Create Status](/#modelscreate_status) query.
