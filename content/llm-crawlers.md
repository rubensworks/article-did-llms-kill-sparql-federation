## AI Crawlers Disrupt Open Data Infrastructure
{:#llm-crawlers}

In recent years, we have seen the rapid rise of generative AI tools such as ChatGPT, Grok, and Copilot.
These rely on [Large Language Models (LLMs)](cite:cites llm) that strongly depend on data that is accessible to them on the Web.
LLMs use this data during their training,
for gathering content in real-time based on user queries,
and agentic actions using across services according to the [Model Context Protocol](cite:cites mcp) (e.g. a user navigating the Web using a headless browser).
Especially this training step requires massive amounts of data,
which involves [crawling large parts of the Web](cite:cites colossalcleancrawledcorpusllm).

[Crawlers](cite:cites webcrawler) have been common since the early days of the Web,
for example to build indexes for powering search engines such as Google and Bing.
However, with the rising popularity of LLM tools,
[the Web is experiencing a large increase in traffic due to AI crawlers](cite:cites cloudflareaitraffic).
While [`robots.txt`](cite:cites robotstxt) has been a common technique for server administrators to tell what data crawlers are allowed to access using which frequency,
[Content Signals](cite:cites contentsignals) are an extension to this to for what purpose LLMs may use content.

Unfortunately, many AI crawlers do not follow these guidelines and are more aggressive than traditional crawlers.
They cause this added traffic to become unmanageable for many Web servers.
As such, administrators that want to avoid their servers being overloaded
have to resort to [mitigation techniques](cite:cites mitigatingllmcrawlertraffic) such as rate limits, human verification, and blocking.
Other initiatives include requiring AI crawlers to [pay per crawl](cite:cites cloudflarepaypercrawl).
Since many crawlers are smart enough to work around such mitigation techniques,
there are even techniques to [trap misbehaving crawlers into AI labyrinths](cite:cites cloudflareailabyrinth).
