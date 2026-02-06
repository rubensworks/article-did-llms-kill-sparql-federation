## Discussion and Future Work
{:#discussion}

AI crawlers are placing open data infrastructure under great pressure.
Our findings show that public SPARQL endpoints are no exception to this,
as well known endpoints are starting to put in place strict rate limits
to be able to cope with this added traffic.
Unfortunately, not only AI crawlers are impacted by this,
but also federated query engines are impacted as an unintended consequence.

The findings above should come with no surprise,
as we have known for a long time that [public SPARQL endpoints have had availability issues](cite:cites sparqlreadyforaction).
Since the recent advancements around LLMs, this existing problem is simply being enlarged.
If we want to publish public Knowledge Graphs in a sustainable manner,
we will have to rethink how we publish and consume Knowledge Graphs.

Due to the rising popularity of LLMs, these rate limits are likely to stay with us long-term.
Hence, there is a [need for a new generation of query planning techniques for SPARQL federation that take into account such restrictions](cite:cites wikidata_federation).
These should depend on new or extended standards that allow these restrictions to be communicated to clients in a machine-readable manner.
The `Retry-After` header and DBpedia's HTML page are steps in the right direction,
but they are only visible to clients after a limit has been exceeded,
while this information would be needed during query planning when discovering the endpoint's capabilities.

Besides quick-fix solutions such as rate limits and API keys,
we may have to more fundamentally alter our publishing approaches.
It may for example be worth it to revisit research towards [alternative low-cost and cache-friendly KG interfaces](cite:cites tpf,brtpf,smartkg,sage,wisekg,passage)
and [link-traversal-based querying over plain Linked Data documents](cite:cites linktraversalfoundations,solidquery),
which come with the trade-off of higher client-side effort when querying.
Or this may be an indication that free access KGs is simply not sustainable,
and that [publishers will have to charge clients per request](cite:cites cloudflarepaypercrawl,solidwebmonetization),
which will require intelligent federated query planning techniques
that take into account total monetary costs within their cost model.

The goal of this position paper is to raise awareness to these issues.
Our findings are based on just a limited set of queries,
so there is certainly a need for more thorough analyses of real-world federation across general and domain-specific endpoints,
whereas existing federation techniques have only been evaluated in context of [closed and ideal scenarios](cite:cites fedbench,largerdfbench)
that lack rate limits and other real-world effects such as timeouts and temporary downtime.
For instance, 657 of the 1573 datasets within the [Linked Open Data Cloud](cite:cites lodcloud) are public SPARQL endpoints at the time of writing,
but it is unknown how many of these endpoints have such restrictions,
and therefore break current SPARQL federation engines.
Furthermore, discussions with KG publishers must be held to determine
if AI crawlers are indeed the main cause of the placement of these restrictions,
or if there are other reasons for putting them in place.
Finally, there is a need for KG publishers and developers of KG consumer software to come together and define best practises
on how to mitigate availability issues originating from AI crawlers.

One of the the main selling points of Knowledge Graphs and the [Semantic Web](cite:cites semanticweb)
is the ability to distribute and interlink data across different data sources,
and integrate them through techniques such as SPARQL federated queries.
However, we are on a trajectory where usage restrictions make it impossible for such federated queries to be executed.
This problem is so significant that one might start questioning the fundamental motivations behind Knowledge Graph technologies.
If we can not integrate data across multiple Knowledge Graphs anymore,
what is their value compared to closed and silo-oriented databases?
