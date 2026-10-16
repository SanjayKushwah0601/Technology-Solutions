# Search 10B Records in Milliseconds

Membership filters that quickly check whether an element might exist in a large dataset, reducing unnecessary disk reads and index lookups.

## Filters

| Filter | Folder | Best when |
| --- | --- | --- |
| [Bloom Filter](./bloom-filter/) | [`bloom-filter/`](./bloom-filter/) | Frequent insertions, general-purpose checks |
| [Cuckoo Filter](./cuckoo-filter/) | [`cuckoo-filter/`](./cuckoo-filter/) | Dynamic data with deletions |
| [XOR Filter](./xor-filter/) | [`xor-filter/`](./xor-filter/) | Static, read-heavy datasets |
| [Binary Fuse Filter](./binary-fuse-filter/) | [`binary-fuse-filter/`](./binary-fuse-filter/) | Large immutable indexes |

## Recommendation

- **Bloom Filter:** General-purpose membership checks with frequent insertions.
- **Cuckoo Filter:** Dynamic datasets requiring deletion support.
- **XOR Filter:** Static datasets requiring fast, memory-efficient lookups.
- **Binary Fuse Filter:** Large, read-heavy datasets where memory efficiency is critical.

**Note:** These filters accelerate membership checks but do not replace a search index. Searching 10 billion records efficiently requires an appropriate indexing strategy, data partitioning, and query optimization.
