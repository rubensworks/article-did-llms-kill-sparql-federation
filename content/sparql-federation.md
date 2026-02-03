## SPARQL Federation Integrates Knowledge Graphs
{:#sparql-federation}

[SPARQL](cite:cites spec:sparqllang) is the standard language for querying over RDF-based Knowledge Graphs (KGs),
with [SPARQL endpoints](cite:cites spec:sparqlprot) being a popular way of exposing access to such KGs through a Web-based API.
Since RDF is based on using global identifiers for resources,
these identifiers can be used and interlinked across multiple distributed KGs.
While each SPARQL endpoint offer queryable access to just a single KG,
[SPARQL federated queries](cite:cites spec:sparqlfederation) allow combining data from multiple endpoints
through `SERVICE` clauses.

As users may not always know exactly which RDF triples originate from what endpoints,
writing these `SERVICE` clauses manually within their query may not always be feasible.
For this reason, various [federation approaches](cite:cites fedx,hibiscus,splendid,anapsid,fedup) exist
to automatically decompose a query to a query with `SERVICE` clauses and join data across multiple SPARQL endpoints efficiently.
Furthermore, federation techniques have also been introduced to [federate over heterogeneous interfaces](cite:cites heterogeneous_fedqpl,heterogeneous_lars,heterogeneous_replicas),
which includes not only SPARQL endpoints, but also interfaces such as [TPF](cite:cites tpf) and [brTPF](cite:cites brtpf).
These techniques are implemented in SPARQL federation engines such as [Comunica](cite:cites comunica) and [HeFQUIN](cite:cites hefquin).
leading to *virtually integrated Knowledge Graphs*,
which can be queried as if the data was centralized.