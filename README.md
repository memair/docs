# docs.memair.com

The developer docs for Memair's GraphQL API. GitHub Pages builds [docs.memair.com](https://docs.memair.com) from `master`.

Each page is a Markdown file in a collection: `_documentation`, `_authentication`, `_graphql` or `_models`. `index.html` renders every page on one long page, ordered by `position`. The first run of code blocks on a page becomes tabs, titled by `{: title="..." }`, and `right_code` in the front matter fills the right-hand column.

The pages explain concepts and conventions and give one or two examples per model. They do not copy the schema: [GraphiQL](https://memair.com/graphiql) is the field reference. Every GraphQL example has to validate against the current schema without deprecated fields, and should run as written with Otto's token where its scopes allow.

Pull requests are welcome.
