## Redshift

Online Analytics Processing (OLAP):
- performing calculations on large record sets

Columnar Data Storage:
- stores data in columns instead of rows which improves performance when performing calculations on data
- far fewer I/Os
- data stored can be compressed much more than row-based databases as data is stored sequentially (advanced compression)
- distributes data and queries across all nodes improving performance (massive parallel processing)
- easy to add and use more nodes as required

### Limitations

- Only avaliable on 1 AZ
    + can restore from snapshot in the event of an outage

### Redshift Configurations

- Single Node: up to 160Gb
- Multi-Node: consists of a Leader node which distributes work (receives client connections and distributes queries) and compute nodes(up to 128 nodes), which store data  and perform queries

### Price Considerations

- Charged for compute nodes, data stored and data transferred