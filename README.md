# Technology Solutions

Technology solutions for problems in coding, system design, and software architecture.

## Contents

| Topic | Folder |
| --- | --- |
| [Search 10B Records in Milliseconds](./search-10b-records/) | [`search-10b-records/`](./search-10b-records/) |
| [Grafana k6](./grafana-k6/) | [`grafana-k6/`](./grafana-k6/) |

### Search 10B Records in Milliseconds

Membership filters that accelerate existence checks before hitting a full search index.

| Filter | Folder |
| --- | --- |
| [Bloom Filter](./search-10b-records/bloom-filter/) | [`bloom-filter/`](./search-10b-records/bloom-filter/) |
| [Cuckoo Filter](./search-10b-records/cuckoo-filter/) | [`cuckoo-filter/`](./search-10b-records/cuckoo-filter/) |
| [XOR Filter](./search-10b-records/xor-filter/) | [`xor-filter/`](./search-10b-records/xor-filter/) |
| [Binary Fuse Filter](./search-10b-records/binary-fuse-filter/) | [`binary-fuse-filter/`](./search-10b-records/binary-fuse-filter/) |

**Note:** These filters accelerate membership checks but do not replace a search index. Searching 10 billion records efficiently requires an appropriate indexing strategy, data partitioning, and query optimization.
