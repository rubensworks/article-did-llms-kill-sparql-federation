## Findings on Public SPARQL Endpoints
{:#public-endpoint-findings}

Since 2018, we have been serving a [Web-based version of the Comunica engine](https://query.comunica.dev/){:.mandatory},
with which users can execute SPARQL queries directly within their Web browser.
This Web client offers example queries, which include several queries that federate over public SPARQL endpoints.
However, within the last year, we have started seeing queries failing, which used to work without any problems.
Hereafter, we discuss three of our queries that started failing,
which includes federation over three of the most popular and largest public SPARQL endpoints:
[Wikidata](cite:cites wikidata), [DBpedia](cite:cites dbpedia), and [Uniprot](cite:cites uniprot).
These three queries can be found in
[](#query-uniprot-rhea), [](#query-wikidata-cats), and [](#query-harvard).
The first two federate purely over SPARQL endpoints,
while the last one federates over a SPARQL endpoints and two [TPF interfaces](cite:cites tpf).

<figure id="query-uniprot-rhea" class="listing">
````/code/query-uniprot-rhea.sparql````
<figcaption markdown="block">
A [federated query](https://query.comunica.dev/#transientDatasources=https%3A%2F%2Fsparql.uniprot.org%2Fsparql;https%3A%2F%2Fsparql.rhea-db.org%2Fsparql&query=PREFIX%20rh%3A%20%3Chttp%3A%2F%2Frdf.rhea-db.org%2F%3E%0APREFIX%20up%3A%20%3Chttp%3A%2F%2Fpurl.uniprot.org%2Fcore%2F%3E%0APREFIX%20taxon%3A%20%3Chttp%3A%2F%2Fpurl.uniprot.org%2Ftaxonomy%2F%3E%0APREFIX%20up%3A%20%3Chttp%3A%2F%2Fpurl.uniprot.org%2Fcore%2F%3E%0A%0A%23%20Query%2013%0A%23%20Select%20all%20Rhea%20reactions%20used%20to%20annotate%20Escherichia%20coli%20%28taxid%3D83333%29%20in%20UniProtKB%2FSwiss-Prot%0A%23%20return%20the%20number%20of%20UniProtKB%20entries%0A%23%20%0A%23%20Federated%20query%20using%20a%20service%20to%20UniProt%20SPARQL%20endpoint%0A%23%20%0A%23%20This%20query%20cannot%20be%20performed%20using%20the%20Rhea%20search%20website%0ASELECT%20%3Funiprot%20%3Fmnemo%20%3Frhea%20%3Faccession%20%3Fequation%20%0AWHERE%20%7B%0A%20%20%7B%20%0A%20%20%20%20VALUES%20%28%3Ftaxid%29%20%7B%20%28taxon%3A83333%29%20%7D%0A%20%20%20%20GRAPH%20%3Chttp%3A%2F%2Fsparql.uniprot.org%2Funiprot%3E%20%7B%0A%20%20%20%20%20%20%3Funiprot%20up%3Areviewed%20true%20.%20%0A%20%20%20%20%20%20%3Funiprot%20up%3Amnemonic%20%3Fmnemo%20.%20%0A%20%20%20%20%20%20%3Funiprot%20up%3Aorganism%20%3Ftaxid%20.%0A%20%20%20%20%20%20%3Funiprot%20up%3Aannotation%2Fup%3AcatalyticActivity%2Fup%3AcatalyzedReaction%20%3Frhea%20.%20%0A%20%20%20%20%7D%0A%20%20%7D%0A%20%20%3Frhea%20rh%3Aaccession%20%3Faccession%20.%0A%20%20%3Frhea%20rh%3Aequation%20%3Fequation%20.%0A%7D) over [Uniprot and Rhea to find Escherichia coli reactions](cite:cites uniprotqueries).
</figcaption>
</figure>

<figure id="query-wikidata-cats" class="listing">
````/code/query-wikidata-cats.sparql````
<figcaption markdown="block">
A [federated query](https://query.comunica.dev/#transientDatasources=https%3A%2F%2Fdbpedia.org%2Fsparql;https%3A%2F%2Fquery.wikidata.org%2Fsparql&query=PREFIX%20wd%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%0APREFIX%20rdfs%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0ASELECT%20*%20WHERE%20%7B%0A%20%20%3Fcat%20wdt%3AP31%20wd%3AQ146%20%3B%0A%20%20%20%20%20%20%20wdt%3AP19%20%5B%20wdt%3AP17%20wd%3AQ30%20%5D%20%3B%20%23%20wd%3AQ695511%0A%20%20%20%20%20%20%20rdfs%3Alabel%20%3Fname%20.%0A%20%20FILTER%28LANG%28%3Fname%29%20%3D%20%22en%22%29%0A%7D) over Wikidata and DBpedia to find all cats in Wikidata.
</figcaption>
</figure>

<figure id="query-harvard" class="listing">
````/code/query-harvard.sparql````
<figcaption markdown="block">
A [federated query](https://query.comunica.dev/#datasources=https%3A%2F%2Fdbpedia.org%2Fsparql&transientDatasources=%2F%2Fdata.linkeddatafragments.org%2Fviaf;%2F%2Fdata.linkeddatafragments.org%2Fharvard&query=SELECT%20%3Fperson%20%3Fname%20%3Fbook%20%3Ftitle%20%7B%0A%20%20%3Fperson%20dbpedia-owl%3AbirthPlace%20%5B%20rdfs%3Alabel%20%22San%20Francisco%22%40en%20%5D.%0A%20%20%3FviafID%20schema%3AsameAs%20%3Fperson%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20schema%3Aname%20%3Fname.%0A%20%20%3Fbook%20dc%3Acontributor%20%5B%20foaf%3Aname%20%3Fname%20%5D%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20dc%3Atitle%20%3Ftitle.%0A%7D) over DBpedia, VIAF (TPF), and Harvard Library (TPF) to find San Franciscans in the Harvard library.
</figcaption>
</figure>

Comunica implements state-of-the-art SPARQL federation algorithms such as [FedX](cite:cites fedx) and [SPLENDID](cite:cites splendid).
In order for a federation engine such as Comunica to execute a SPARQL query,
the engine has to split up the original SPARQL query into several smaller queries,
which are sent to different endpoints,
after which results are joined together locally within the federation engine.
Depending on the complexity of the query, dataset size, and the used federation algorithms,
the number of HTTP requests to the SPARQL endpoints can vary greatly.

While Comunica could successfully execute the queries above in the past,
it is not able to anymore,
even though no relevant code changes were made since then.
When executing any of the queries within Comunica,
the engine errors and stops execution after just a few seconds,
and reports HTTP 429 (Too Many Requests) errors from the SPARQL endpoints.
This starts occurring after 34 HTTP requests (0.7 seconds) for the query in [](#query-uniprot-rhea),
116 requests (0.9 seconds) for [](#query-wikidata-cats),
and 30 requests (0.5 seconds) for [](#query-harvard).

Both Uniprot and Wikidata report the text `Rate Limit Exceeded` within their HTTP response body.
While Wikidata provides no further information on this rate limit,
Uniprot returns the `Retry-After: 10` header, indicating the client should wait for 10 seconds before another request can be made.
DBpedia provides some more information in the form of an HTML page,
which says that the site is configured to allow `100 simultaneous connections from the same IP address` 
and `50 requests per second from the same IP address`,
and advises the user to `Please try again soon`.
These rate limits appear to have been enabled within the last year,
or have at least been lowered significantly.

While these are just the results of 3 example queries,
we see the same problems occurring for other federated queries over public endpoints.
