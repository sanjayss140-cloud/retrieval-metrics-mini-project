# Evaluation Results and Interpretation

## Results Table

| Query | Keyword rank | Semantic rank |
|---|---|---|
| my redis cache keeps showing old data | 8 | 1 |
| how do I add semantic search to a table I already have | miss | 2 |
| redis or memcached for caching | 1 | 2 |
| why did my query get slower after I added an index | miss | 1 |
| what does ACID actually guarantee | 2 | 1 |
| how do I keep my postgres online while changing the schema | 6 | 3 |
| my background jobs stop after every deploy | miss | 2 |
| how do I let my database accept more writes per second | 4 | 1 |
| sql or nosql for a new product | 1 | 3 |
| why does my redis memory keep climbing | miss | 2 |
| **Summary** | **MRR 0.30 · Recall@10 0.60** | **MRR 0.67 · Recall@10 1.00** |

## Interpretation

Overall, semantic search is clearly superior across both metrics, achieving an MRR of 0.67 compared to keyword search's 0.30, and finding relevant documents in the top 10 for every single query with a Recall@10 of 1.00 versus 0.60 for keyword search. Keyword search won on exact-term, entity-comparison queries such as "redis or memcached for caching" (rank 1 vs 2) and "sql or nosql for a new product" (rank 1 vs 3), which both feature well-defined, distinct technical keywords directly matching the document vocabulary. In contrast, semantic search dominated queries describing conversational questions, failure symptoms, or troubleshooting problems like "why did my query get slower after I added an index" (rank 1 vs miss), "my background jobs stop after every deploy" (rank 2 vs miss), and "how do I let my database accept more writes per second" (rank 1 vs 4), where the meaning and intent matter far more than literal word overlap. Engineering teams should still keep the keyword search system around rather than discarding it entirely because the two systems have complementary strengths, making a hybrid search system (such as BM25 + Vector with Reciprocal Rank Fusion) capable of outperforming either individual approach.
