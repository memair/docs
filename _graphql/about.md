---
title: About GraphQL
position: 1.0
description: GraphQL is a powerful API query language
---

GraphQL is a data query language which provides an alternative to REST and ad-hoc web service architectures. It allows clients to define the structure of the data required, and exactly the same structure of the data is returned from the server. It is a strongly typed runtime which allows clients to dictate what data is needed, therefore preventing excessively large amounts of data being returned.

Memair's implementation of GraphQL allows for bulk record retrieval, single record creation, multiple record creation (up to 100 records per request; processed immediately), and bulk record creation (up to 10,000 records per request; processed in the background).
