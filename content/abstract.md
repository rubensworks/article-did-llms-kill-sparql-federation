## Abstract
<!-- Context      -->
RDF provides the basis for distributing Knowledge Graphs (KGs) across different locations,
which is useful when KGs
cover different data domains with varying purposes,
are managed by different teams and organizations,
or are exposed by different access policies.
One of the most popular ways of publishing a KG is through a SPARQL endpoint,
which offers queryable access.
When multiple of these KGs need to be integrated,
techniques such as SPARQL federation can be used.
<!-- Need         -->
While many KGs have been available as public SPARQL endpoints,
their openness is currently being challenged
by the huge load that is placed on them by modern LLM crawlers.
Recently, public SPARQL endpoints have started putting in place usage restrictions
to avoid going down under this increased server load.
While these restrictions limit the range of SPARQL queries that can be executed over them,
it becomes especially problematic for SPARQL federated queries,
which often involves sending multiple smaller queries to endpoints in a short timeframe.
<!-- Task         -->
The goal of this position paper is to raise the alarm regarding the state of SPARQL federation,
as many **federated SPARQL queries that used to work, simply can not be executed anymore** with state of the art techniques.
<!-- Object       -->
In this article, we discuss where and how these restrictions have been put in place,
and possible mitigations strategies.
<!-- Findings     -->
<!-- Conclusion   -->
<!-- Perspectives -->
Through this, we aim to trigger discussions about the sustainability of public KG infrastructure,
and challenge future research towards new querying or publishing techniques that can cope with this new reality.
