# How to Dump Elasticsearch Indexes

### Pre-read

[https://www.npmjs.com/package/elasticdump](https://www.npmjs.com/package/elasticdump)\
[https://www.elastic.co/guide/index.html](https://www.elastic.co/guide/index.html)

### Prerequisites

* [elasticdump](https://www.npmjs.com/package/elasticdump)&#x20;
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) is a CLI to connect to the kubernetes cluster from your machine

### Steps:

1.  Exec into the playground pod of you environment

    `kubectl exec` -it`<playground_pod_name> -n playground -- bash`&#x20;
2. Install elasticdump client if it's not available in the playground pod
3.  The indexes available in an Elasticsearch environment can be known as follows&#x20;

    `curl http://`elasticsearch-data-v1.es-cluster:9200`/_cat/indices?v`
4.  ES indexes can be dumped to a JSON file which can then be restored in the otherr environment.

    `elasticdump --input=http://elasticsearch-data-v1.es-cluster:9200/<my_index> --output=<my_index>.json`

    **`Note`**`: Replace <my_index> with your index name that you need to take dump`
5. Zip the dump and download the dump into your local machine
   1. install the zip if it's not available in the playground pod
      1. zip es-dump.zip \<my\_index>.json
   2. Run the below command from your local machine to download the es dump&#x20;
      1. `kubectl cp playground/<POD_NAME>:/root/es-dump.zip $HOME/es-dump.zip`
6. The same can be restored in the other environment as follows&#x20;
   1.  Copy the es dump from your local machine to another environment's playground pod

       `kubectl cp $HOME/es-dump.zip playground/<POD_NAME>:/root/es-dump.zip $HOME/es-dump.zip`
   2.  Restore the es index dump

       `elasticdump --input= <my_index>.json --output=http://elasticsearch-data-v1.es-cluster:9200/<my_index>`

### Troubleshooting

Sometimes, the following error is thrown when indexes are getting restored.

`error: {`

`type: 'cluster_block_exception',`

`reason: 'blocked by: [FORBIDDEN/12/index read-only / allow delete (api)];'`

`}`

This occurs because in its default configuration, Elasticsearch will not allocate any more disk space when more than 90% of the disk is used overall. (i.e. by Elasticsearch or other applications). This watermark can be set lower but this may prevent important applications from being able to properly allocate disk space.

A way out is to increase the size of the destination ES cluster (according to the size of the source cluster).

The capacity of the ES cluster (for the source/destination end) can be checked as follows :

`curl -XGET 'http://elasticsearch-data-v1.es-cluster:9200/_cat/allocation?v'`

If, for example, the elasticsearch-data uses a PersistentVolumeClaim, the same can be edited to increase the size using edit pvc PVC name. This capacity can only be increased if the underlying storage class has AllowVolumeExpansion set to true.

\
\
