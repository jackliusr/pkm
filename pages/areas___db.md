- consistency model
  ![](https://jepsen.io/consistency/models/map.svg)
- Living without atomic clocks: Where CockroachDB and Spanner diverge
- [### Timestamp Oracle](https://dzone.com/articles/tidbs-timestamp-oracle)
- [Hybrid logical clock](https://www.cse.buffalo.edu/tech-reports/2014-04.pdf) (HLC)
- log based replication
- change data capture (CDC)
- fill-factor: provided for fine-tuning index data storage and performance. When an index is created or rebuilt, the fill-factor value **determines the percentage of space on each leaf-level page to be filled with data**, reserving the remainder on each page as free space for future growth.