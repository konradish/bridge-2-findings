# Qdrant Dual-Index for the Gut — Phase 3 Design

## The integration

Qdrant natively supports named vectors — multiple vectors per point, each with independent dimensionality and distance metric. This makes the gut's dual-index retrieval a first-class Qdrant feature, not a hack.

## Collection schema

```json
{
  "vectors": {
    "text": {
      "size": 384,
      "distance": "Cosine"
    },
    "gut": {
      "size": 8,
      "distance": "Cosine"
    }
  }
}
```

Text embeddings (384-dim from the existing embedding model) and gut vectors (8-dim from the minGRU) live on the same point. Both are queryable independently.

## Storage format per memory point

```json
{
  "id": "content_hash",
  "vector": {
    "text": [0.1, 0.2, ...],    // 384-dim semantic embedding
    "gut": [2.87, 5.97, ...]     // 8-dim gut state at time of storage
  },
  "payload": {
    "text": "the memory content",
    "source": "finding",
    "tags": ["contra", "alignment"],
    "date": "2026-03-14",
    "stored_at": "2026-03-14T06:00:00"
  }
}
```

## Retrieval modes

1. **Text-only** (current behavior): `query=[text_embedding], using="text"` — "find memories about this topic"
2. **Gut-only** (new): `query=[gut_vector], using="gut"` — "find memories from similar conversational states"
3. **Hybrid** (Qdrant prefetch): search both, fuse with RRF — "find memories that are both topically and somatically relevant"

## Migration path

Option A: Create `bridge_memory_v2` with named vectors, re-ingest everything with both embeddings. Keep `bridge_memory` as fallback.

Option B: Delete and recreate `bridge_memory`. Simpler but destructive.

**Recommendation:** Option A. The existing 665+ points keep working. New points get both vectors. Gut retrieval is available on any point that has a gut vector.

## Implementation steps

1. Create `bridge_memory_v2` collection with named vector schema
2. Modify `memory_search.py store` to also compute gut vector for the current conversation state and store both
3. Add `--mode text|gut|hybrid` flag to `memory_search.py search`
4. Re-ingest existing points with text vectors only (gut vectors will be null for historical data — that's fine, Qdrant handles sparse named vectors)

## The evaluation question

How do we know gut retrieval is better? Compare:
- For a set of queries, retrieve top-5 by text and top-5 by gut
- Score: are the gut-retrieved memories relevant? Are they DIFFERENT from text-retrieved?
- The value is in the difference — gut should surface memories that text would miss

---

Sources:
- Qdrant named vectors: https://qdrant.tech/documentation/concepts/vectors/
- Qdrant hybrid queries: https://qdrant.tech/documentation/concepts/hybrid-queries/
